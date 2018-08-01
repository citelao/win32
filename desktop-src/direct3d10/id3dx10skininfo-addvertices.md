---
Description: Allocate space for additional vertices.
ms.assetid: dd6445ea-4754-4ba3-a264-59295325ee08
title: ID3DX10SkinInfo::AddVertices method
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
topic_type: 
- APIRef
- kbSyntax
api_name: 
- ID3DX10SkinInfo.AddVertices
api_type: 
- COM
api_location: 
- D3DX10.lib
- D3DX10.dll
---

# ID3DX10SkinInfo::AddVertices method

Allocate space for additional vertices.

## Syntax


```C++
HRESULT AddVertices(
  [in] UINT Count
);
```



## Parameters

<dl> <dt>

*Count* \[in\]
</dt> <dd>

Type: **[**UINT**](https://msdn.microsoft.com/en-us/library/Aa383751(v=VS.85).aspx)**

The number of vertices to add.

</dd> </dl>

## Return value

Type: **[**HRESULT**](https://msdn.microsoft.com/en-us/library/Bb401631(v=MSDN.10).aspx)**

If this method succeeds, the return value is S\_OK. If the method fails, the return value can be: E\_OUTOFMEMORY.

## Requirements



|                    |                                                                                       |
|--------------------|---------------------------------------------------------------------------------------|
| Header<br/>  | <dl> <dt>D3DX10.h</dt> </dl>   |
| Library<br/> | <dl> <dt>D3DX10.lib</dt> </dl> |



## See also

<dl> <dt>

[ID3DX10SkinInfo](id3dx10skininfo.md)
</dt> <dt>

[D3DX Interfaces](d3d10-graphics-reference-d3dx10-interfaces.md)
</dt> </dl>

 

 



