---
title: How to Create a Radial Gradient Brush
description: Shows how to create a radial gradient brush using Direct2D.
ms.assetid: 663743c9-16e9-4e3a-90b2-883ef0b8d5cf
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# How to Create a Radial Gradient Brush

To create a radial gradient brush, use the [**ID2DRenderTarget::CreateRadialGradientBrush**](/windows/desktop/api/d2d1/nf-d2d1-createradialgradientbrush) method and specify the radial gradient brush properties and the gradient stop collection. Some overloads enable you to specify the brush properties. The following code shows how to create a radial gradient brush to fill a circle, and a solid black brush to draw the outline of the circle.

The code produces the output shown in the following illustration.

![illustration of a circle filled with a radial gradient brush](images/brushes-ovw-radials.png)

1.  Declare a variable of type [**ID2D1RadialGradientBrush**](https://msdn.microsoft.com/en-us/library/Dd371529(v=VS.85).aspx).
    ```C++
        ID2D1RadialGradientBrush *m_pRadialGradientBrush;
    ```

    

2.  Create an array of [**D2D1\_GRADIENT\_STOP**](/windows/desktop/api/d2d1/ns-d2d1-d2d1_gradient_stop) structures to put in the gradient stop collection. The **D2D1\_GRADIENT\_STOP** structure contains the position and color of a gradient stop. The position indicates the relative position of the gradient stop in the brush. The value is in the range \[0.0f, 1.0f\], as shown in the following code.

    ```C++
    // Create an array of gradient stops to put in the gradient stop
    // collection that will be used in the gradient brush.
    ID2D1GradientStopCollection *pGradientStops = NULL;

    D2D1_GRADIENT_STOP gradientStops[2];
    gradientStops[0].color = D2D1::ColorF(D2D1::ColorF::Yellow, 1);
    gradientStops[0].position = 0.0f;
    gradientStops[1].color = D2D1::ColorF(D2D1::ColorF::ForestGreen, 1);
    gradientStops[1].position = 1.0f;
    // Create the ID2D1GradientStopCollection from a previously
    // declared array of D2D1_GRADIENT_STOP structs.
    hr = m_pRenderTarget->CreateGradientStopCollection(
        gradientStops,
        2,
        D2D1_GAMMA_2_2,
        D2D1_EXTEND_MODE_CLAMP,
        &pGradientStops
        );
    ```

    

3.  Use the [**ID2D1RenderTarget::CreateGradientStopCollection**](https://msdn.microsoft.com/en-us/library/Dd742781(v=VS.85).aspx) method to create the [**ID2D1GradientStopCollection**](https://msdn.microsoft.com/en-us/library/Dd316783(v=VS.85).aspx) collection from a previously declared array of [**D2D1\_GRADIENT\_STOP**](/windows/desktop/api/d2d1/ns-d2d1-d2d1_gradient_stop) structures. Then, Use the [**CreateRadialGradientBrush**](/windows/desktop/api/d2d1/nf-d2d1-createradialgradientbrush) to create a radial gradient brush.

    > [!Note]  
    > Starting with Windows 8, you can use the [**ID2D1DeviceContext::CreateGradientStopCollection**](https://msdn.microsoft.com/en-us/library/Hh404502(v=VS.85).aspx) method to create a [**ID2D1GradientStopCollection1**](https://msdn.microsoft.com/en-us/library/Hh446792(v=VS.85).aspx) collection instead of the [**ID2D1RenderTarget::CreateGradientStopCollection**](https://msdn.microsoft.com/en-us/library/Dd742781(v=VS.85).aspx) method. This interface adds high-color gradients and the interpolation of gradients in either straight or prmultiplied colors. See the **ID2DDeviceContext::CreateGradientStopCollection** page for more information.

     

    ```C++
    // The center of the gradient is in the center of the box.
    // The gradient origin offset was set to zero(0, 0) or center in this case.
    if (SUCCEEDED(hr))
    {
        hr = m_pRenderTarget->CreateRadialGradientBrush(
            D2D1::RadialGradientBrushProperties(
                D2D1::Point2F(75, 75),
                D2D1::Point2F(0, 0),
                75,
                75),
            pGradientStops,
            &m_pRadialGradientBrush
            );
    }
    ```

    

    ```C++
    m_pRenderTarget->FillEllipse(ellipse, m_pRadialGradientBrush);
    m_pRenderTarget->DrawEllipse(ellipse, m_pBlackBrush, 1, NULL);
    ```

    

## Related topics

<dl> <dt>

[Direct2D Reference](reference.md)
</dt> </dl>

 

 



