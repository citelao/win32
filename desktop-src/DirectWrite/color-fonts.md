---
title: Color Fonts
description: This topic describes color fonts, their support in DirectWrite and Direct2D, and how to use them in your app.
ms.assetid: 74e096c4-9d1c-8854-e9ee-f8b11ac1c71a
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# Color Fonts

This topic describes color fonts, their support in DirectWrite and Direct2D, and how to use them in your app.

This document contains the following parts:

-   [What are color fonts?](#what-are-color-fonts)
-   [Why use color fonts?](#why-use-color-fonts)
-   [What kinds of color fonts does Windows support?](#what-kinds-of-color-fonts-does-windows-support)
-   [Using color fonts](#using-color-fonts)
    -   [Using color fonts in a XAML app](#using-color-fonts-in-a-xaml-app)
    -   [Using color fonts in Microsoft Edge](#using-color-fonts-in-microsoft-edge)
    -   [Using color fonts with DirectWrite and Direct2D](#using-color-fonts-with-directwrite-and-direct2d)
    -   [Using color fonts with Win2D](#using-color-fonts-with-win2d)
-   [Related topics](#related-topics)

## What are color fonts?

Color fonts, also referred to as  multicolored fonts  or  chromatic fonts,  are a font technology that allows font designers to use multiple colors within each glyph. Color fonts enable multicolored text scenarios in apps and websites with less code and more robust operating system support than ad-hoc techniques implemented above the text rendering system.

Most fonts for reading and writing the fonts you are probably most familiar with are not color fonts. These fonts define only the shape of the glyphs they contain, either with vector outlines or monochromatic bitmaps. At draw time, a text renderer fills the glyph shape using a single color (the  font color ) specified by the app or document being rendered. Color fonts, on the other hand, contain color information in addition to shape information. Some approaches allow font designers to offer multiple color palettes, giving the color font artistic flexibility.

The following example shows a glyph from the Segoe UI Emoji color font. The glyph is rendered in monochrome on the left, and in color on the right.

![](images/color-font-cat.png)

Color fonts typically include fallback information for platforms that do not support color fonts or for scenarios in which color functionality has been disabled. On those platforms, color fonts are rendered as regular monochromatic fonts.

## Why use color fonts?

Historically, designers and developers have used a variety of techniques to achieve multicolored text. For example, websites often use raster images instead of text in order to display rich headers. This approach enables artistic flexibility, but raster graphics do not scale well to all display sizes, nor do they provide the same accessibility features as real text. Another common technique is to overlay multiple monochromatic fonts in different font colors, but this typically requires extra layout code to manage.

Color fonts offer a way to achieve these visual effects with all the simplicity and functionality of regular fonts. Text rendered in a color font is the same as other text: it can be copied and pasted, it can be parsed by accessibility tools, and so forth.

## What kinds of color fonts does Windows support?

The [OpenType specification](https://www.microsoft.com/Typography/OpenTypeSpecification.aspx) defines several ways to embed color information in a font. Starting in Windows 10 Anniversary Update, DirectWrite and Direct2D (and the Windows frameworks built on them) support all of these approaches. They are summarized in the table below:



| Technique                                                                                                                        | Description                                                                                                                                                                                                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [COLR](https://www.microsoft.com/typography/otspec/colr.md)/[CPAL](https://www.microsoft.com/typography/otspec/cpal.md) tables | Uses layers of colored vectors, whose shapes are defined in the same way as single-color glyph outlines. **Note:** Supported starting in Windows 8.1. <br/>                                                                                                                                                 |
| [SVG](https://www.microsoft.com/typography/otspec/svg.md) table                                                                 | Uses vector images authored in the Scalable Vector Graphics format. **Note:** As of Windows 10 Anniversary Update, DirectWrite supports a subset of the full SVG spec. Not all SVG content is guaranteed to render in an OpenType SVG font. See [SVG Support](https://msdn.microsoft.com/library/windows/desktop/mt790715) for more details. <br/> |
| [CBDT](https://www.microsoft.com/typography/otspec/cbdt.md)/[CBLC](https://www.microsoft.com/typography/otspec/cblc.md) tables | Uses embedded color bitmap images.                                                                                                                                                                                                                                                                                |
| [sbix](https://www.microsoft.com/typography/otspec/sbix.md) table                                                               | Uses embedded color bitmap images.                                                                                                                                                                                                                                                                                |



 

## Using color fonts

From the user s perspective, color fonts are  just fonts . For example, they can usually be installed and uninstalled from the system in the same way as monochromatic fonts, and they are rendered as regular, selectable text.

From the developer s perspective too, color fonts are usually used the same way as monochromatic fonts. In the XAML and Microsoft Edge frameworks, you can style your text with color fonts the same way as regular fonts, and by default your text will be rendered in color. However, if your app directly calls Direct2D APIs (or Win2D APIs) to render text, it must explicitly request color font rendering.

### Using color fonts in a XAML app

The XAML platform s text elements (such as [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx), [TextBox](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textbox.aspx), [RichEditBox](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.richeditbox.aspx), [Glyphs](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.documents.glyphs.aspx?f=255&MSPPError=-2147217396), and [FontIcon](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.fonticon.aspx)) support color fonts by default. Simply style your text with a color font, and any color glyphs will be rendered in color. The following code example shows one way to style a TextBlock with a color font packaged with your app. The same technique applies to regular fonts.


```XML
<TextBlock FontFamily="Assets/TMyColorFont.otf#MyFontFamilyName">Here is some text.</TextBlock>
```



If you never want your XAML text element to render multicolored text, set its [IsColorFontEnabledProperty](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.iscolorfontenabledproperty.aspx) property to false.

### Using color fonts in Microsoft Edge

Color fonts are rendered by default in websites and web apps running on Microsoft Edge, including the XAML [WebView](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.webview.aspx) control. Simply use HTML and CSS to style your text with a color font, and any color glyphs will be rendered in color.

### Using color fonts with DirectWrite and Direct2D

Your app can use Direct2D s higher-level text drawing methods ([**DrawText**](https://msdn.microsoft.com/library/windows/desktop/mt761993) and [**DrawTextLayout**](https://msdn.microsoft.com/library/windows/desktop/mt750187)) or it can use lower-level techniques to draw glyph runs directly. In either case, your app requires code changes in order to handle color glyphs correctly. If your app uses Direct2D s **DrawText** and **DrawTextLayout** APIs, note that these do not render color glyphs by default. This is to avoid unexpected behavior changes in text rendering apps that were designed prior to color font support.

To opt in to color glyph rendering, pass the [**D2D1\_DRAW\_TEXT\_OPTIONS\_ENABLE\_COLOR\_FONT**](https://msdn.microsoft.com/library/windows/desktop/dd368095) options flag to the drawing method. The following code example shows how to call Direct2D s DrawText method to render a string in a color font:


```C++
// If m_textFormat points to a font with color glyphs, then the following  
// call will render m_string using the color glyphs available in that font. 
// Any monochromatic glyphs will be rendered with m_defaultFillBrush. 
m_deviceContext->DrawText( 
    m_string->Data(), 
    m_string->Length(), 
    m_textFormat.Get(), 
    m_layoutRect, 
    m_defaultFillBrush.Get(), 
    D2D1_DRAW_TEXT_OPTIONS_ENABLE_COLOR_FONT 
    );  
    
```



If your app uses lower-level APIs to handle glyph runs directly, then it will continue to function in the presence of color fonts, but it will not be able to draw color glyphs without additional logic.

To correctly handle color glyphs, your app should:

1.  Pass the glyph run information to [**TranslateColorGlyphRun**](https://msdn.microsoft.com/en-us/library/Mt761992(v=VS.85).aspx), along with a [**DWRITE\_GLYPH\_IMAGE\_FORMATS**](/windows/desktop/api/dcommon/ne-dcommon-dwrite_glyph_image_formats) parameter that indicates which type(s) of color glyph the app is prepared to handle. If any color glyphs are present (based on the font and the requested **DWRITE\_GLYPH\_IMAGE\_FORMATS**), then DirectWrite will split the primary glyph run into individual  color glyph runs  which can be accessed through the returned [**IDWriteColorGlyphRunEnumerator**](idwritecolorglyphrunenumerator.md) object in Step 4.
2.  Check the HRESULT returned by [**TranslateColorGlyphRun**](https://msdn.microsoft.com/en-us/library/Mt761992(v=VS.85).aspx) to determine whether any color glyph runs were detected. An **HRESULT** of **DWRITE\_E\_NOCOLOR** indicates no applicable color glyph run.
3.  If [**TranslateColorGlyphRun**](https://msdn.microsoft.com/en-us/library/Mt761992(v=VS.85).aspx) reported no color glyph runs (by returning **DWRITE\_E\_NOCOLOR**), then the whole glyph run is treated as monochromatic, and your app should draw it as desired (for example, using [**ID2D1DeviceContext::DrawGlyphRun**](https://msdn.microsoft.com/library/windows/desktop/hh404508)).
4.  If [**TranslateColorGlyphRun**](https://msdn.microsoft.com/en-us/library/Mt761992(v=VS.85).aspx) does report the presence of color glyph runs, then your app should ignore the primary glyph run and instead use the color glyph run(s) returned by TranslateColorGlyphRun. To do so, iterate through the returned [**IDWriteColorGlyphRunEnumerator1**](https://msdn.microsoft.com/en-us/library/Mt725314(v=VS.85).aspx) object, retrieving each color glyph run and drawing it as appropriate for its glyph image format (for example, you can use [**DrawColorBitmapGlyphRun**](https://msdn.microsoft.com/library/windows/desktop/mt750184) and [**DrawSvgGlyphRun**](https://msdn.microsoft.com/library/windows/desktop/mt750185) to draw color bitmap glyphs and SVG glyphs, respectively).

The following code example shows the general structure of this procedure:


```C++
// An example code snippet demonstrating how to use TranslateColorGlyphRun 
// to handle different kinds of color glyphs. This code does not make any 
// actual drawing calls. 
HRESULT DrawGlyphRun( 
    FLOAT baselineOriginX, 
    FLOAT baselineOriginY, 
    DWRITE_MEASURING_MODE measuringMode, 
    _In_ DWRITE_GLYPH_RUN const* glyphRun, 
    _In_ DWRITE_GLYPH_RUN_DESCRIPTION const* glyphRunDescription, 
) 
{ 
    // Specify the color glyph formats your app supports. In this example, 
    // the app requests only glyphs defined with PNG or SVG. 
    DWRITE_GLYPH_IMAGE_FORMATS requestedFormats = 
        DWRITE_GLYPH_IMAGE_FORMATS_PNG | DWRITE_GLYPH_IMAGE_FORMATS_SVG; 

    ComPtr<IDWriteColorGlyphRunEnumerator1> glyphRunEnumerator; 
    HRESULT hr = m_dwriteFactory->TranslateColorGlyphRun( 
        D2D1::Point2F(baselineOriginX, baselineOriginY), 
        glyphRun, 
        glyphRunDescription, 
        requestedFormats, // the glyph formats supported by this renderer 
        measuringMode, 
        nullptr, 
        0, 
        &glyphRunEnumerator // on return, may contain color glyph runs 
        ); 

    if (hr == DWRITE_E_NOCOLOR) 
    { 
        // The glyph run has no color glyphs. Draw it as a monochrome glyph 
        // run, for example using the DrawGlyphRun method on a Direct2D 
        // device context. 
    } 
    else 
    { 
        // The glyph run has one or more color glyphs. 
        DX::ThrowIfFailed(hr); 

        // Iterate through the color glyph runs and draw them. 
        for (;;) 
        { 
            BOOL haveRun; 
            DX::ThrowIfFailed(glyphRunEnumerator->MoveNext(&haveRun)); 
            if (!haveRun) 
            { 
                break; 
            } 

            // Retrieve the color glyph run. 
            DWRITE_COLOR_GLYPH_RUN1 const* colorRun; 
            DX::ThrowIfFailed(glyphRunEnumerator->GetCurrentRun(&colorRun)); 

            // Draw the color glyph run depending on its format. 
            switch (colorRun->glyphImageFormat) 
            { 
            case DWRITE_GLYPH_IMAGE_FORMATS_PNG: 
                // Draw the PNG glyph, for example with 
                // ID2D1DeviceContext4::DrawColorBitmapGlyphRun. 
                break; 

            case DWRITE_GLYPH_IMAGE_FORMATS_SVG: 
                // Draw the SVG glyph, for example with 
                // ID2D1DeviceContext4::DrawSvgGlyphRun. 
                break; 

                // ...etc. 
            } 
        } 
    } 

    return hr; 
} 
```



### Using color fonts with Win2D

Similar to Direct2D, Win2D s text drawing APIs do not render color glyphs by default. To opt in to color glyph rendering, set the [EnableColorFont](http://microsoft.github.io/Win2D/html/T_Microsoft_Graphics_Canvas_Text_CanvasDrawTextOptions.md) options flag in the text format object your app passes to the text drawing method. The following code example shows how to render a string in a color font using Win2D:


```C++
// The text format that will be used to draw the text. (Declared elsewhere 
// and initialized elsewhere by the app to point to a color font.) 
CanvasTextFormat m_textFormat; 

// Set the EnableColorFont option. 
m_textFormat.Options = CanvasDrawTextOptions.EnableColorFont; 

// If m_textFormat points to a font with color glyphs, then the following  
// call will render m_string using the color glyphs available in that font. 
// Any monochromatic glyphs will be rendered with m_color. 
args.DrawingSession.DrawText( 
    m_string, 
    m_point, 
    m_color, 
    m_textFormat 
    ); 
    
```



## Related topics

[DirectWrite color glyph sample](http://go.microsoft.com/fwlink/p/?LinkId=832476)


[DirectWrite Color Font Fallback sample](https://code.msdn.microsoft.com/windowsapps/DirectWrite-Color-Font-ef762d88)


[**IDWriteFontFace4 interface**](https://msdn.microsoft.com/en-us/library/Mt725320(v=VS.85).aspx)


[**IDWriteFactory4::TranslateColorGlyphRun method**](https://msdn.microsoft.com/en-us/library/Mt761992(v=VS.85).aspx)


[**ID2D1DeviceContext4::DrawText method**](https://msdn.microsoft.com/library/windows/desktop/mt761993)


 

 




