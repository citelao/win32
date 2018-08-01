---
Description: Uses a user-provided function to fill each texel of each mip level of a given texture.
ms.assetid: 9c822472-2bbf-4629-bdb3-6491573e8de2
title: D3DXFillTexture function
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
topic_type:
- APIRef
- kbSyntax
api_name:
- D3DXFillTexture
api_type:
- LibDef
api_location:
- d3dx9.lib
- d3dx9.dll
---

# D3DXFillTexture function

Uses a user-provided function to fill each texel of each mip level of a given texture.

## Syntax


```C++
HRESULT D3DXFillTexture(
  _Out_ LPDIRECT3DTEXTURE9 pTexture,
  _In_  LPD3DXFILL2D       pFunction,
  _In_  LPVOID             pData
);
```



## Parameters

<dl> <dt>

*pTexture* \[out\]
</dt> <dd>

Type: **[**LPDIRECT3DTEXTURE9**](https://msdn.microsoft.com/library/Bb205909(v=VS.85).aspx)**

Pointer to an [**IDirect3DTexture9**](https://msdn.microsoft.com/library/Bb205909(v=VS.85).aspx) interface, representing the filled texture.

</dd> <dt>

*pFunction* \[in\]
</dt> <dd>

Type: **[LPD3DXFILL2D](lpd3dxfill2d.md)**

Pointer to a user-provided evaluator function, which will be used to compute the value of each texel. The function follows the prototype of [LPD3DXFILL2D](lpd3dxfill2d.md).

</dd> <dt>

*pData* \[in\]
</dt> <dd>

Type: **[**LPVOID**](https://msdn.microsoft.com/en-us/library/Aa383751(v=VS.85).aspx)**

Pointer to an arbitrary block of user-defined data. This pointer will be passed to the function provided in *pFunction*.

</dd> </dl>

## Return value

Type: **[**HRESULT**](https://msdn.microsoft.com/en-us/library/Bb401631(v=MSDN.10).aspx)**

If the function succeeds, the return value is D3D\_OK. If the function fails, the return value can be one of the following values: D3DERR\_INVALIDCALL.

## Remarks

Here is an example that creates a function called ColorFill, which relies on D3DXFillTexture.


```
// Define a function that matches the prototype of LPD3DXFILL3D
VOID WINAPI ColorFill (D3DXVECTOR4* pOut, const D3DXVECTOR2* pTexCoord, 
const D3DXVECTOR2* pTexelSize, LPVOID pData)
{
    *pOut = D3DXVECTOR4(pTexCoord->x, pTexCoord->y, 0.0f, 0.0f);
}
    
    
// Fill the texture using D3DXFillTexture
if (FAILED (hr = D3DXFillTexture (m_pTexture, ColorFill, NULL)))
{
    return hr;
}
```



## Requirements



|                    |                                                                                       |
|--------------------|---------------------------------------------------------------------------------------|
| Header<br/>  | <dl> <dt>D3dx9tex.h</dt> </dl> |
| Library<br/> | <dl> <dt>D3dx9.lib</dt> </dl>  |



## See also

<dl> <dt>

[Texture Functions in D3DX 9](dx9-graphics-reference-d3dx-functions-texture.md)
</dt> </dl>

 

 



