---
title: How to Use Rich Edit Text Operations
description: An application can send messages to retrieve or find text in a rich edit control. You can retrieve either the selected text or a specified range of text.
ms.assetid: 95D88F9A-3DD1-48E4-B6FF-3168F2D25846
ms.technology: desktop
ms.prod: windows
ms.author: windowssdkdev
ms.topic: article
ms.date: 05/31/2018
---

# How to Use Rich Edit Text Operations

An application can send messages to retrieve or find text in a rich edit control. You can retrieve either the selected text or a specified range of text.

To get the selected text in a rich edit control, use the [**EM\_GETSELTEXT**](em-getseltext.md) message. The text is copied to the specified character array. You must ensure that the array is large enough to hold the selected text plus a terminating null character.

To retrieve a specified range of text, use the [**EM\_GETTEXTRANGE**](em-gettextrange.md) message. The [**TEXTRANGE**](/windows/desktop/api/Richedit/ns-richedit-_textrange) structure used with this message specifies the text range to retrieve and points to a character array that receives the text. Here again, the application must ensure that the array is large enough for the specified text plus a terminating null character.

You can search for a string in a rich edit control by using the [**EM\_FINDTEXT**](em-findtext.md) or [**EM\_FINDTEXTEX**](em-findtextex.md) messages, or their Unicode equivalents, [**EM\_FINDTEXTW**](em-findtextw.md) and [**EM\_FINDTEXTEXW**](em-findtextexw.md). The [**FINDTEXT**](/windows/desktop/api/Richedit/ns-richedit-_findtext) structure that is used with the nonextended versions specifies the text range to search and the string to search for. The extended versions use a [**FINDTEXTEX**](/windows/desktop/api/Richedit/ns-richedit-_findtextexa) structure, which specifies the same information and also receives the start and end points of the character range of the found text. You can also specify such options as whether the search is case sensitive.

## What you need to know

### Technologies

-   [Windows Controls](window-controls.md)

### Prerequisites

-   C/C++
-   Windows User Interface Programming

## Instructions

### Use a Rich Edit Text Operation

The following example function finds the specified text within the selected text in a rich edit control that supports Unicode. If the target is found, it becomes the new selection.


```C++
BOOL FindTextInSelection(HWND hRich, WCHAR* target)
{
    CHARRANGE selectionRange;
    
    SendMessage(hRich, EM_EXGETSEL, 0, (LPARAM)&selectionRange);
    
    FINDTEXTEX ftex;
    
    ftex.lpstrText  = target;
    ftex.chrg.cpMin = selectionRange.cpMin;
    ftex.chrg.cpMax = selectionRange.cpMax;
    
    LRESULT lr = SendMessage(hRich, EM_FINDTEXTEXW, (WPARAM)FR_DOWN, (LPARAM) &ftex);
    
    if (lr >= 0)
    {
        LRESULT lr1 = SendMessage(hRich, EM_EXSETSEL, 0, (LPARAM)&ftex.chrgText);
        
        SendMessage(hRich, EM_HIDESELECTION, (LPARAM)FALSE, 0);
        
        return TRUE;
    }
    
    return FALSE;
    
}
```



## Remarks

Microsoft Rich Edit 3.0 also supports the HexToUnicode Input Method Editor (IME) function, which allows a user to convert between hexadecimal and Unicode by using hot keys. For more information, see [HexToUnicode IME](https://msdn.microsoft.com/library/windows/desktop/dd318146).

## Related topics

<dl> <dt>

[Using Rich Edit Controls](using-rich-edit-controls.md)
</dt> <dt>

[Windows common controls demo (CppWindowsCommonControls)](http://go.microsoft.com/fwlink/p/?linkid=214295)
</dt> </dl>

 

 



