﻿---
title: JET_RETRIEVECOLUMN members (Microsoft.Isam.Esent.Interop)
TOCTitle: JET_RETRIEVECOLUMN members
ms:assetid: AllMembers.T:Microsoft.Isam.Esent.Interop.JET_RETRIEVECOLUMN
ms:mtpsurl: https://msdn.microsoft.com/en-us/library/microsoft.isam.esent.interop.jet_retrievecolumn_members(v=EXCHG.10)
ms:contentKeyID: 55103877
ms.date: 07/30/2014
ms.topic: article
---

# JET\_RETRIEVECOLUMN members

Include protected members  
Include inherited members  

Contains input and output parameters for [JetRetrieveColumns(JET\_SESID, JET\_TABLEID, \[\], Int32)](dn334004\(v=exchg.10\).md). Fields in the structure describe what column value to retrieve, how to retrieve it, and where to save results.

The [JET\_RETRIEVECOLUMN](dn351033\(v=exchg.10\).md) type exposes the following members.

## Constructors

<table>
<thead>
<tr class="header">
<th> </th>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="images/Dn292146.pubmethod(EXCHG.10).gif" title="Public method" alt="Public method" /></td>
<td><a href="dn351036(v=exchg.10).md">JET_RETRIEVECOLUMN</a></td>
<td></td>
</tr>
</tbody>
</table>


Top

## Properties

<table>
<thead>
<tr class="header">
<th> </th>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="images/Dn292128.pubproperty(EXCHG.10).gif" title="Public property" alt="Public property" /></td>
<td><a href="dn335226(v=exchg.10).md">cbActual</a></td>
<td>Gets the size, in bytes, of data that is retrieved by a retrieve column operation.</td>
</tr>
<tr class="even">
<td><img src="images/Dn292128.pubproperty(EXCHG.10).gif" title="Public property" alt="Public property" /></td>
<td><a href="dn335228(v=exchg.10).md">cbData</a></td>
<td>Gets or sets the size of the <a href="dn351040(v=exchg.10).md">pvData</a> buffer, in bytes. The retrieve column operation will not store more data in pvData than cbData.</td>
</tr>
<tr class="odd">
<td><img src="images/Dn292128.pubproperty(EXCHG.10).gif" title="Public property" alt="Public property" /></td>
<td><a href="dn335230(v=exchg.10).md">columnid</a></td>
<td>Gets or sets the column identifier for the column to retrieve.</td>
</tr>
<tr class="even">
<td><img src="images/Dn292128.pubproperty(EXCHG.10).gif" title="Public property" alt="Public property" /></td>
<td><a href="dn335229(v=exchg.10).md">columnidNextTagged</a></td>
<td>Gets the columnid of the tagged, multi-valued, or sparse column when all tagged columns are retrieved by passing 0 as the columnid.</td>
</tr>
<tr class="odd">
<td><img src="images/Dn292128.pubproperty(EXCHG.10).gif" title="Public property" alt="Public property" /></td>
<td><a href="dn335231(v=exchg.10).md">err</a></td>
<td>Gets the warning returned from the retrieval of the column.</td>
</tr>
<tr class="even">
<td><img src="images/Dn292128.pubproperty(EXCHG.10).gif" title="Public property" alt="Public property" /></td>
<td><a href="dn335232(v=exchg.10).md">grbit</a></td>
<td>Gets or sets the options for column retrieval.</td>
</tr>
<tr class="odd">
<td><img src="images/Dn292128.pubproperty(EXCHG.10).gif" title="Public property" alt="Public property" /></td>
<td><a href="dn335233(v=exchg.10).md">ibData</a></td>
<td>Gets or sets the offset in the buffer that data will be stored in.</td>
</tr>
<tr class="even">
<td><img src="images/Dn292128.pubproperty(EXCHG.10).gif" title="Public property" alt="Public property" /></td>
<td><a href="dn335234(v=exchg.10).md">ibLongValue</a></td>
<td>Gets or sets the offset to the first byte to be retrieved from a column of type <a href="hh577895(v=exchg.10).md">LongBinary</a> or <a href="hh577895(v=exchg.10).md">LongText</a>.</td>
</tr>
<tr class="odd">
<td><img src="images/Dn292128.pubproperty(EXCHG.10).gif" title="Public property" alt="Public property" /></td>
<td><a href="dn351039(v=exchg.10).md">itagSequence</a></td>
<td>Gets or sets the sequence number of the values that are contained in a multi-valued column. If the itagSequence is 0 then the number of instances of a multi-valued column are returned instead of any column data.</td>
</tr>
<tr class="even">
<td><img src="images/Dn292128.pubproperty(EXCHG.10).gif" title="Public property" alt="Public property" /></td>
<td><a href="dn351040(v=exchg.10).md">pvData</a></td>
<td>Gets or sets the buffer that will store data that is retrieved from the column.</td>
</tr>
</tbody>
</table>


Top

## Methods

<table>
<thead>
<tr class="header">
<th> </th>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><img src="images/Dn292146.pubmethod(EXCHG.10).gif" title="Public method" alt="Public method" /></td>
<td><a href="http://msdn2.microsoft.com/en-us/library/bsc2ak47">Equals</a></td>
<td>(Inherited from <a href="http://msdn2.microsoft.com/en-us/library/e5kfa45b">Object</a>.)</td>
</tr>
<tr class="even">
<td><img src="images/Dn292116.protmethod(EXCHG.10).gif" title="Protected method" alt="Protected method" /></td>
<td><a href="http://msdn2.microsoft.com/en-us/library/4k87zsw7">Finalize</a></td>
<td>(Inherited from <a href="http://msdn2.microsoft.com/en-us/library/e5kfa45b">Object</a>.)</td>
</tr>
<tr class="odd">
<td><img src="images/Dn292146.pubmethod(EXCHG.10).gif" title="Public method" alt="Public method" /></td>
<td><a href="http://msdn2.microsoft.com/en-us/library/zdee4b3y">GetHashCode</a></td>
<td>(Inherited from <a href="http://msdn2.microsoft.com/en-us/library/e5kfa45b">Object</a>.)</td>
</tr>
<tr class="even">
<td><img src="images/Dn292146.pubmethod(EXCHG.10).gif" title="Public method" alt="Public method" /></td>
<td><a href="http://msdn2.microsoft.com/en-us/library/dfwy45w9">GetType</a></td>
<td>(Inherited from <a href="http://msdn2.microsoft.com/en-us/library/e5kfa45b">Object</a>.)</td>
</tr>
<tr class="odd">
<td><img src="images/Dn292116.protmethod(EXCHG.10).gif" title="Protected method" alt="Protected method" /></td>
<td><a href="http://msdn2.microsoft.com/en-us/library/57ctke0a">MemberwiseClone</a></td>
<td>(Inherited from <a href="http://msdn2.microsoft.com/en-us/library/e5kfa45b">Object</a>.)</td>
</tr>
<tr class="even">
<td><img src="images/Dn292146.pubmethod(EXCHG.10).gif" title="Public method" alt="Public method" /></td>
<td><a href="dn335224(v=exchg.10).md">ToString</a></td>
<td>Returns a <a href="http://msdn2.microsoft.com/en-us/library/s1wwdcbf">String</a> that represents the current <a href="dn351033(v=exchg.10).md">JET_RETRIEVECOLUMN</a>. (Overrides <a href="http://msdn2.microsoft.com/en-us/library/7bxwbwt2">Object.ToString()</a>.)</td>
</tr>
</tbody>
</table>


Top

## See also

#### Reference

[JET\_RETRIEVECOLUMN class](dn351033\(v=exchg.10\).md)

[Microsoft.Isam.Esent.Interop namespace](hh596136\(v=exchg.10\).md)
