<div xmlns="http://www.w3.org/1999/xhtml" class="chapter"><div class="titlepage"><div><div><h2 class="title"><a name="chapter.cmap"></a>Chapter 5. cmap - Character to Glyph Index Mapping Table</h2></div></div></div><div role="specification" class="section"><div class="titlepage"><div><div><h3 class="title"><a name="section.6.1"></a>Specification</h3></div></div></div><p>This table specifies how character codes in an input text should
          be mapped to glyph indices. The table may contain more than one mapping,
          to support a variety of character encoding schemes used by font consumers. Each mapping is stored in a subtable, and the table header
          indicates the character encodings for which subtables are present.
      </p><div class="section"><div class="titlepage"><div><div><h4 class="title"><a name="section.6.1.1"></a>Header</h4></div></div></div><p>The Character To Glyph Index Mapping Table begins with
        a header.</p><div class="table"><a name="idm1698"></a><p class="title"><strong>Table 5.1. cmap Header</strong></p><div class="table-contents"><table class="table" summary="cmap Header" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>version</td><td>Table version number (0).</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>numTables</td><td>Number of encoding records.</td><td class="auto-generated"> </td></tr><tr><td>EncodingRecord</td><td>encodingRecords[numTables]</td><td>Encoding records.</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>The encoding records specify an encoding and
    the offset to the subtable for that encoding, as follows:</p><div class="table"><a name="idm1720"></a><p class="title"><strong>Table 5.2. Encoding Record</strong></p><div class="table-contents"><table class="table" summary="Encoding Record" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>platformID</td><td>Platform ID.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>encodingID</td><td>Platform-specific encoding ID.</td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>offset</td><td>Byte offset to subtable.</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>The <a class="link" href="chapter.common_structures.html#common_structures.platformencoding" title="Platform and Encoding Identifiers">platform
        ID and platform-specific encoding ID</a> values in the
          encoding record are used to specify the character repertoire and
          encoding used by the subtable.
        </p><p>Subtables also contain a language ID field. For
          <a class="link" href="chapter.cmap.html" title="Chapter 5. cmap - Character to Glyph Index Mapping Table">cmap</a> subtables with platform ID 1 (Macintosh)
          which contain language-specific mappings, this ID field must be set
          to the
          <a class="link" href="chapter.common_structures.html#common_structures.languageid" title="Language Identifiers">Macintosh language ID</a>
          of the language <span class="emphasis"><em>plus one</em></span>.
          Otherwise, the language ID field must be set to zero.
        </p><p>Encoding records in the cmap table header must be sorted first by
          platform ID, then by platform-specific encoding ID, and then by
          language ID in the corresponding subtable. Each platform
          ID, platform-specific encoding ID, and language ID
          combination must appear only once in the
          <a class="link" href="chapter.cmap.html" title="Chapter 5. cmap - Character to Glyph Index Mapping Table">cmap</a> table.</p><p>The offset is measured from the start of the cmap table.</p></div></div><div role="fragment deprecated" class="section"><div class="titlepage"><div><div><h3 class="title"><a name="cmap_cust"></a>OTF Windows NT compatibility mapping</h3></div></div></div><div role="specification" class="section"><div class="titlepage"><div><div><h4 class="title"><a name="section.6.2.1"></a>Specification</h4></div></div></div><p>If a platform ID 4 (custom), encoding ID 0-255 (OTF
          Windows NT compatibility mapping) <a class="link" href="chapter.cmap.html" title="Chapter 5. cmap - Character to Glyph Index Mapping Table">cmap</a>
          encoding is present in an CommonType font with CFF outlines,
          then the OTF font driver in Windows NT will: (a) superimpose
          the glyphs encoded at character codes 0-255 in the encoding
          on the corresponding Windows ANSI (code page 1252) Unicode
          values in the Unicode encoding it reports to the system; (b)
          add Windows ANSI (CharSet 0) to the list of CharSets
          supported by the font; and (c) consider the value of the
          encoding ID to be a Windows CharSet value and add it to the
          list of CharSets supported by the font.</p><p>This <a class="link" href="chapter.cmap.html" title="Chapter 5. cmap - Character to Glyph Index Mapping Table">cmap</a> encoding provides a
          compatibility mechanism for non-Unicode applications that use
          the font as if it were Windows ANSI encoded.</p></div></div><div class="section"><div class="titlepage"><div><div><h3 class="title"><a name="section.6.3"></a>cmap Subtable Formats</h3></div></div></div><div role="fragment" class="section"><div class="titlepage"><div><div><h4 class="title"><a name="idm1760"></a>Format 0: Byte encoding table</h4></div></div></div><div role="specification" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.1.1"></a>Specification</h5></div></div></div><p>This is a simple character to glyph index mapping table. It is
        limited to 256 character codepoints and can only access glyph IDs
        between 0 and 255.
      </p><div class="table"><a name="idm1765"></a><p class="title"><strong>Table 5.3. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>format</td><td>Format number is set to 0.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>length</td><td>Length in bytes of the subtable.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>language</td><td>Language ID (for Macintosh language-specific mappings)</td><td class="auto-generated"> </td></tr><tr><td>BYTE</td><td>glyphIdArray[256]</td><td>An array that maps character codes to glyph
              index values.</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>Font producers must include 256 elements in the glyphIdArray
        and set the length to 262. Glyph consumers, however, must read the
        length field and read either (length - 6) glyph IDs or 256, whichever
        is the less.
      </p><div class="section"><div class="titlepage"><div><div><h6 class="title"><a name="section.6.3.1.1.1"></a>Mapping Process for Font Consumers</h6></div></div></div><p>
          To map codepoints to glyph IDs in a format 0 subtable, each input
          codepoint is used to index the glyphIdArray to retrieve a glyph ID.
          Before indexing the array, the font consumer must ensure that the input
          codepoint is less than the number of entries in the glyphIdArray;
          if it is not less, then the character is mapped to glyph index 0.
        </p></div></div></div><div role="fragment" class="section"><div class="titlepage"><div><div><h4 class="title"><a name="idm1793"></a>Format 2: High-byte mapping through table </h4></div></div></div><div role="specification" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.2.1"></a>Specification</h5></div></div></div><p>This subtable is designed to faciliate mapping characters to glyphs
          within the encoding mechanisms which use a mixed 8/16-bit encoding,
          such as the legacy national character code standards used for Japanese,
          Chinese, and Korean characters.
      </p><p>In a mixed encoding, codepoints may be represented either by a one
          byte integer or a two byte integer, with certain values of the initial
          byte acting as a continuation signal.</p><div class="table"><a name="idm1799"></a><p class="title"><strong>Table 5.4. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>format</td><td>Format number is set to 2.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>length</td><td>Length in bytes of the subtable.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>language</td><td>Language ID (for Macintosh language-specific mappings)</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>subHeaderKeys [256]</td><td>Array that maps high bytes to subHeaders:
              value is subHeader index * 8.</td><td class="auto-generated"> </td></tr><tr><td>4 words struct</td><td>subHeaders []</td><td>Variable-length array of subHeader
              structures.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>glyphIndexArray []</td><td>Variable-length array containing subarrays
              used for mapping the low byte of 2-byte
              characters.</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>A subHeader is structured as follows:</p><div class="table"><a name="idm1832"></a><p class="title"><strong>Table 5.5. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>firstCode</td><td>First valid low byte for this
              subHeader.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>entryCount</td><td>Number of valid low bytes for this
              subHeader.</td><td class="auto-generated"> </td></tr><tr><td>SHORT</td><td>idDelta</td><td>See text below.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>idRangeOffset</td><td>See text below.</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>The firstCode and entryCount values specify the range of low-byte
          values handled by this subheader. Bytes outside of this range are
          mapped to glyph index 0.
      </p><p>
          The value of idRangeOffset points to the element of the
          glyphElement array corresponding to the firstCode. Note that
          unlike most offset values in this standard, the idRangeOffset
          counts the number of bytes from <span class="emphasis"><em>the byte position of
          the idRangeOffset record itself</em></span> to the target element,
          rather than from the start of the subtable header.
      </p><p>
          The value of idDelta specifies a delta to be added the glyph ID,
          modulo 65536, to permit the same range to be used for several
          different subheaders.
      </p><p>subHeader 0 must contain the following values:</p><div class="informaltable"><table class="informaltable" border="1"><colgroup><col/><col/></colgroup><tbody><tr><td>firstCode</td><td>0</td></tr><tr><td>entryCount</td><td>256</td></tr><tr><td>idDelta</td><td>0</td></tr><tr><td>idRangeOffset</td><td>offset to start of glyphIndexArray</td></tr></tbody></table></div><div class="section"><div class="titlepage"><div><div><h6 class="title"><a name="section.6.3.2.1.1"></a>Mapping Process for Font Consumers</h6></div></div></div><p>
          To map codepoints to glyph IDs in a format 0 subtable, the font
          consumer should consume the input character stream one byte at a time,
          and perform the following sequence of operations.
        </p><p>
          First, the input byte is used to index the subHeaderKeys array to
          obtain a <span class="emphasis"><em>subheader key</em></span>.
        </p><p>
          Where the subheader key is 0, this indicates that the
          input byte is the only byte in this codepoint. The input byte is
          then directly looked up in the glyphIndexArray to obtain the glyph ID.
        </p><p>
          Where the subheader key is greater than 0, this indicates a two-byte
          character. First, the subheader key should be divided by 8,
          and the font consumer should then use this to index into the subheader
          array to obtain the appropriate subheader.
        </p><p>
          Next, the font consumer should consume another input byte, the <span class="emphasis"><em>low byte</em></span>, and ensure that the value of the low byte is within
          the range of this subheader - that is, that the low byte is more than or
          equal to firstCode and less than firstCode+entryCount. If the low byte
          is not within the range of the subheader, glyph ID 0 is returned.
        </p><p>firstCode is then subtracted from the low byte to determine the
          <span class="emphasis"><em>index offset</em></span>. The font consumer will then advance
          idRangeOffset bytes from the position of the idRangeOffset element in
          the subheader to find the beginning of the glyph mapping subrange, and
          then also advance by the index offset to determine the glyph ID.</p><p>Finally, if the glyph ID is non-zero and idDelta is non-zero,
          idDelta is added to the glyph ID module 65536 to return the final glyph ID.
        </p></div></div></div><div role="fragment" class="section"><div class="titlepage"><div><div><h4 class="title"><a name="idm1888"></a>Format 4: Segment mapping to delta values</h4></div></div></div><div role="specification" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.3.1"></a>Specification</h5></div></div></div><p>This format is used to map Unicode characters in the Basic
          Multilingual Plane. It is used when the codepoints to be mapped
          can be divided into several contiguous ranges or <span class="emphasis"><em>segments</em></span>. The segments may include codepoints which are not mapped
          to glyphs.
        </p><p>
          The subtable has three parts. First, a header which includes parameters
          for an optimized search of the segment list:</p><div class="table"><a name="idm1895"></a><p class="title"><strong>Table 5.6. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>format</td><td>Format number is set to 4.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>length</td><td>Length in bytes of the subtable.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>language</td><td>Language ID (for Macintosh language-specific mappings)</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>segCountX2</td><td>2 x segCount.</td><td class="auto-generated"> </td></tr><tr role="deprecated"><td>USHORT</td><td>searchRange</td><td>2 x (2**floor(log2(segCount)))</td><td class="auto-generated"> </td></tr><tr role="deprecated"><td>USHORT</td><td>entrySelector</td><td>log2(searchRange/2)</td><td class="auto-generated"> </td></tr><tr role="deprecated"><td>USHORT</td><td>rangeShift</td><td>2 x segCount - searchRange</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>The number of segments is specified by segCount, which
          is not explicitly in the header; however, all of the header
          parameters are derived from it. The searchRange value is
          twice the largest power of 2 that is less than or equal to
          segCount.</p><p>After the header, four parallel arrays describe the segments:</p><div class="table"><a name="idm1933"></a><p class="title"><strong>Table 5.7. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>endCode [segCount]</td><td>End characterCode for each segment,
              last=0xFFFF.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>reservedPad</td><td>Set to 0.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>startCode [segCount]</td><td>Start character code for each
              segment.</td><td class="auto-generated"> </td></tr><tr><td>SHORT</td><td>idDelta [segCount]</td><td>Delta for all character codes in
              segment.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>idRangeOffset [segCount]</td><td>Offsets into glyphIdArray or 0</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>
          Note that
          unlike most offset values in this standard, the idRangeOffset
          counts the number of bytes from <span class="emphasis"><em>the byte position of
          the idRangeOffset record itself</em></span> to the target element,
          rather than from the start of the subtable header.
        </p><p>
          The final segment must have an endCode value of 0xFFFF.
          This segment need not contain any valid mappings, but must be present.
        </p><p>Finally, there is a variable-length array of glyph IDs.</p><div class="table"><a name="idm1965"></a><p class="title"><strong>Table 5.8. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>glyphIdArray []</td><td>Glyph index array (arbitrary length)
            </td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>
          The segment values are specified in four parallel arrays.
          Each segment is described by a startCode and endCode,
          along with an idDelta and an idRangeOffset, which are used
          for mapping the character codes in the segment. The segments
          are sorted in order of increasing endCode values.
      </p></div><div class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.3.2"></a>Mapping Process for Font Consumers</h5></div></div></div><p>
          To map codepoints to glyph IDs in a format 4 subtable, the font
          consumer should first search the segment arrays for the first endCode
          that is greater than or equal to the codepoint to be mapped. If the
          corresponding startCode is less than or equal to the character code,
          then the segment contains a mapping for this codepoint. Otherwise,
          the missing glyph ID 0 is returned.
        </p><p>
          XXX this para and next still needs rewriting.
          If the idRangeOffset value for the segment is not 0, the
          mapping of character codes relies on glyphIdArray. The
          character code offset from startCode is added to the
          idRangeOffset value. This sum is used as an offset from the
          current location within idRangeOffset itself to index out
          the correct glyphIdArray value. This obscure indexing trick
          works because glyphIdArray immediately follows idRangeOffset
          in the font file. The C expression that yields the glyph
          index is:</p><div class="literallayout"><p><br/>
  *(idRangeOffset[i]/2<br/>
    + (c - startCode[i])<br/>
    + &amp;idRangeOffset[i])<br/>
    </p></div><p>The value c is the character code in question, and i is
          the segment index in which c appears. If the value obtained
          from the indexing operation is not 0 (which indicates
          missingGlyph), idDelta[i] is added to it to get the glyph
          index. The idDelta arithmetic is modulo 65536.</p><p>If the idRangeOffset is 0, the idDelta value is added
          directly to the codepoint modulo 65536 (i.e. (idDelta[i] + c)%65536)
          and the value is returned as the glyph ID.</p></div><div role="discussion" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.3.3"></a>Discussion</h5></div></div></div><p>Here is an example of filling in the header information for a table
        with 39 segments:
      </p><div class="informaltable"><table class="informaltable" border="1"><colgroup><col/><col/><col/></colgroup><tbody><tr><td>segCountX2</td><td>78</td><td> </td></tr><tr><td>searchRange</td><td>64</td><td>(2 * largest power of 2 &lt;=39)</td></tr><tr><td>entrySelector</td><td>5</td><td>log2 (32)</td></tr><tr><td>rangeShift</td><td>14</td><td>2 x 39 - 64</td></tr></tbody></table></div><p>
        That said, the searchRange, entrySelector and rangeShift fields are
        ignored by all current implementations, and should be treated as unused.
      </p><p>
        Uniscribe will fail if the final segment does not have an endCode
        of 0xFFFF, but other implementations will succeed.
      </p><p>As an example of the mapping process, a subtable which maps
          codepoints 10-20, 30-90, and 153-480 onto a contiguous range
          of glyph indices may look like this:</p><div class="informaltable"><table class="informaltable" border="1"><colgroup><col/><col/><col/><col/><col/></colgroup><tbody><tr><td>segCountX2:</td><td>8</td><td> </td><td> </td><td> </td></tr><tr><td>searchRange:</td><td>8</td><td> </td><td> </td><td> </td></tr><tr><td>entrySelector:</td><td>4</td><td> </td><td> </td><td> </td></tr><tr><td>rangeShift:</td><td>0</td><td> </td><td> </td><td> </td></tr><tr><td>endCode:</td><td>20</td><td>90</td><td>480</td><td>0Xffff</td></tr><tr><td>reservedPad:</td><td>0</td><td> </td><td> </td><td> </td></tr><tr><td>startCode:</td><td>10</td><td>30</td><td>153</td><td>0Xffff</td></tr><tr><td>idDelta:</td><td>-9</td><td>-18</td><td>-80</td><td>1</td></tr><tr><td>idRangeOffset:</td><td>0</td><td>0</td><td>0</td><td>0</td></tr></tbody></table></div><p>This table performs the following mappings:</p><div class="literallayout"><p><br/>
10 -&gt; 10 - 9 = 1<br/>
20 -&gt; 20 - 9 = 11<br/>
30 -&gt; 30 - 18 = 12<br/>
90 -&gt; 90 - 18 = 72<br/>
153 -&gt; 153 - 80 = 73<br/>
...and so on.<br/>
</p></div></div></div><div role="fragment" class="section"><div class="titlepage"><div><div><h4 class="title"><a name="idm2069"></a>Format 6: Trimmed table mapping </h4></div></div></div><div role="specification" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.4.1"></a>Specification</h5></div></div></div><div class="table"><a name="idm2073"></a><p class="title"><strong>Table 5.9. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>format</td><td>Format number is set to 6.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>length</td><td>This is the length in bytes of the
              subtable.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>language</td><td>Please see <a class="link" href="">Note
                on the language field in cmap subtables</a> in
              this document.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>firstCode</td><td>First character code of
              subrange.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>entryCount</td><td>Number of character codes in
              subrange.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>glyphIdArray [entryCount]</td><td>Array of glyph index values for character
              codes in the range. </td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>The firstCode and entryCount values specify a subrange
          (beginning at firstCode, length = entryCount) within the
          range of possible character codes. Codes outside of this
          subrange are mapped to glyph index 0. The offset of the code
          (from the first code) within this subrange is used as index
          to the glyphIdArray, which provides the glyph index
          value.</p></div><div role="annotation" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.4.2"></a>Annotation</h5></div></div></div><p>It is unclear whether the entryCount can be 0. We assume
          it can and recommend to add a sentence to that
          effect.</p><p>This format is very similar to format 0, in that there
          is an explicit list of glyph indices for a contiguous range
          of character code. However, there are two intersting
          properties: the range can be bigger than 256; and more
          importantly, the glyph indices are USHORT instead of
          BYTE. So this format can be used for byte encodings to reach
          glyphs other than the first 256 glyphs.</p></div></div><div role="fragment" class="section"><div class="titlepage"><div><div><h4 class="title"><a name="idm2112"></a>Format 8: mixed 16-bit and 32-bit coverage</h4></div></div></div><div role="specification" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.5.1"></a>Specification</h5></div></div></div><p>Format 8 is a bit like format 2, in that it provides for
          mixed-length character codes. If a font contains characters
          from the Unicode Surrogates Area (U+D800-U+DFFF), which are
          UCS-4 characters; it's likely that it will also include
          other, regular 16-bit Unicodes as well. We therefore need a
          format to map a mixture of 16-bit and 32-bit character
          codes, just as format 2 allows a mixture of 8-bit and 16-bit
          codes. A simplifying assumption is made: namely, that there
          are no 32-bit character codes which share the same first 16
          bits as any 16-bit character code. This means that the
          determination as to whether a particular 16-bit value is a
          standalone character code or the start of a 32-bit character
          code can be made by looking at the 16-bit value directly,
          with no further information required.</p><p>Here's the format 8 subtable format:</p><div class="table"><a name="idm2118"></a><p class="title"><strong>Table 5.10. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>format</td><td>Subtable format; set to 8.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>reserved</td><td>Reserved; set to 0</td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>length</td><td>Byte length of this subtable (including the
              header)</td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>language</td><td>Please see <a class="link" href="">Note
                on the language field in cmap subtables</a> in
              this document.</td><td class="auto-generated"> </td></tr><tr><td>BYTE</td><td>is32 [8192]</td><td>Tightly packed array of bits (8K bytes total)
              indicating whether the particular 16-bit (index) value
              is the start of a 32-bit character code
                </td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td> nGroups</td><td> Number of groupings which follow
            </td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>Here follow the individual groups. Each group has the
          following format:</p><div class="table"><a name="idm2153"></a><p class="title"><strong>Table 5.11. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>ULONG</td><td> startCharCode</td><td> First character code in this group; note
              that if this group is for one or more 16-bit character
              codes (which is determined from the is32 array), this
              32-bit value will have the high 16-bits set to zero
            </td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td> endCharCode</td><td> Last character code in this group; same
              condition as listed above for the startCharCode
                </td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td> startGlyphID</td><td> Glyph index corresponding to the starting
              character code </td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>A few notes here. The endCharCode is used, rather than a
          count, because comparisons for group matching are usually
          done on an existing character code, and having the
          endCharCode be there explicitly saves the necessity of an
          addition per group. Groups must be sorted by increasing
          startCharCode. A group's endCharCode must be less than the
          startCharCode of the following group, if any.</p><p>To determine if a particular word (cp) is the first half
          of 32-bit code points, one can use an expression such as (
          is32[ cp / 8 ] &amp; ( 1 &lt;&lt; ( 7 - ( cp % 8 ) ) ) ). If this is
          non-zero, then the word is the first half of a 32-bit code
          point.</p><p>0 is not a special value for the high word of a 32-bit
          code point. A font may not have both a glyph for the code
          point 0x0000 and glyphs for code points with a high word of
          0x0000.</p><p>The presence of the packed array of bits indicating
          whether a particular 16-bit value is the start of a 32-bit
          character code is useful even when the font contains no
          glyphs for a particular 16-bit start value. This is because
          the system software often needs to know how many bytes ahead
          the next character begins, even if the current character
          maps to the missing glyph. By including this information
          explicitly in this table, no "secret" knowledge needs to be
          encoded into the OS.</p><p>Although this format might work advantageously on some
          platforms for non-Unicode encodings, Microsoft does not
          support it for Unicode encoded UCS-4 characters.</p></div><div role="annotation" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.5.2"></a>Annotation</h5></div></div></div><p>First paragraph, second sentence, should be: "If a font
          maps Unicode supplemental characters, it's likely to map
          Unicode BMP characters as well."</p><p>For coherence with the other formats, the description of
          the format field should be "Format number is set to 8" and
          the description of the length field should be "This is the
          length in bytes of the subtable."</p><p>This format is dubious and would probably best be
          deprecated. If For Unicode encodings, it is useful only for
          UTF-16 (the only version that has 16 bit code units), so
          spending 8K bytes to is

If the intent is really for a Unicode encodings,
          then it is known </p></div></div><div role="fragment" class="section"><div class="titlepage"><div><div><h4 class="title"><a name="idm2183"></a>Format 10: Trimmed array</h4></div></div></div><div role="specification" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.6.1"></a>Specification</h5></div></div></div><p>Format 10 is a bit like format 6, in that it defines a
        trimmed array for a tight range of 32-bit character
        codes:</p><div class="table"><a name="idm2188"></a><p class="title"><strong>Table 5.12. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>format</td><td>Subtable format; set to 10.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>reserved</td><td>Reserved; set to 0</td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>length</td><td>Byte length of this subtable (including the
              header) </td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>language</td><td>Please see <a class="link" href="">Note
                on the language field in cmap subtables</a> in
              this document.</td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td> startCharCode</td><td> First character code covered </td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td> numChars</td><td> Number of character codes covered
            </td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td> glyphs []</td><td> Array of glyph indices for the character
              codes covered </td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>This format is not supported by Microsoft.</p></div><div role="annotation" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.6.2"></a>Annotation</h5></div></div></div><p>For coherence with the other formats, the description of
        the format field should be "Format number is set to 10" and the
        description of the length field should be "This is the length
        in bytes of the subtable."</p></div></div><div role="fragment" class="section"><div class="titlepage"><div><div><h4 class="title"><a name="idm2230"></a>Format 12: Segmented coverage</h4></div></div></div><div role="specification" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.7.1"></a>Specification</h5></div></div></div><p>This is the Microsoft standard character to glyph index
          mapping table for fonts supporting the UCS-4 characters in
          the Unicode Surrogates Area (U+D800 - U+DFFF). It is a bit
          like format 4, in that it defines segments for sparse
          representation in 4-byte character space. Here's the
          subtable format:</p><div class="table"><a name="idm2235"></a><p class="title"><strong>Table 5.13. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>format</td><td>Subtable format; set to 12.</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>reserved</td><td>Reserved; set to 0</td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>length</td><td>Byte length of this subtable (including the
              header) </td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>language</td><td>Please see <a class="link" href="">Note
                on the language field in cmap subtables</a> in
              this document.</td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>nGroups</td><td>Number of groupings which follow
            </td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>Fonts providing Unicode encoded UCS-4 character support
          for Windows 2000 and later, need to have a subtable with
          platform ID 3, platform specific encoding ID 1 in format 4;
          and in addition, need to have a subtable for platform ID 3,
          platform specific encoding ID 10 in format 12. Please note,
          that the content of format 12 subtable, needs to be a super
          set of the content in the format 4 subtable. The format 4
          subtable needs to be in the cmap table to enable backward
          compatibility needs.</p><p>Here follow the individual groups, each of which has the
          following format:</p><div class="table"><a name="idm2267"></a><p class="title"><strong>Table 5.14. </strong></p><div class="table-contents"><table class="table" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>ULONG</td><td>startCharCode</td><td>First character code in this group
            </td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>endCharCode</td><td>Last character code in this group
            </td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>startGlyphID</td><td>Glyph index corresponding to the starting
              character code </td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>Groups must be sorted by increasing startCharCode. A
          group's endCharCode must be less than the startCharCode of
          the following group, if any. The endCharCode is used, rather
          than a count, because comparisons for group matching are
          usually done on an existing character code, and having the
          endCharCode be there explicitly saves the necessity of an
          addition per group.</p></div><div role="annotation" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.7.2"></a>Annotation</h5></div></div></div><p>First paragraph, first sentence should be reworded: "...
          for fonts supporting Unicode supplemental characters."
          Similarly, second paragraph, first sentence should be
          reworded: "Fonts providing support for Unicode supplemental
          characters..."</p><p>For coherence with the other formats, the description of
          the format field should be "Format number is set to 12" and
          the description of the length field should be "This is the
          length in bytes of the subtable."</p></div></div><div role="fragment" class="section"><div class="titlepage"><div><div><h4 class="title"><a name="idm2292"></a>Format 14: Unicode Variation Sequences</h4></div></div></div><div role="specification" class="section"><div class="titlepage"><div><div><h5 class="title"><a name="section.6.3.8.1"></a>Specification</h5></div></div></div><p>Subtable format 14 specifies the Unicode Variation
        Sequences (UVSes) supported by the font. A Variation Sequence,
        according to the Unicode Standard, comprises a base character
        followed by a variation selector; e.g. &lt;U+82A6,
        U+E0101&gt;.</p><p>The subtable partitions the UVSes supported by the font
        into two categories: “default” and
        “non-default” UVSes. Given a UVS, if the glyph
        obtained by looking up the base character of that sequence in
        the Unicode cmap subtable (i.e. the UCS-4 or the BMP cmap
        subtable) is the glyph to use for that sequence, then the
        sequence is a “default” UVS; otherwise it is a
        “non-defaultJ=f UVS, and the glyph to use for that
        sequence is specified in the format 14 subtable itself.</p><p>The example below shows how a font vendor can use format
        14 for a JIS-2004-aware font.</p><div class="table"><a name="idm2299"></a><p class="title"><strong>Table 5.15. Format 14 header</strong></p><div class="table-contents"><table class="table" summary="Format 14 header" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>USHORT</td><td>format</td><td>Subtable format; set to 14.</td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>length</td><td>Byte length of this subtable (including the
              header) </td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>numVarSelectorRecords</td><td>Number of Variation Selector Records</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>This is immediately followed by 'numVarSelectorRecords'
        Variation Selector Records.</p><div class="table"><a name="idm2321"></a><p class="title"><strong>Table 5.16. Variation Selector Record</strong></p><div class="table-contents"><table class="table" summary="Variation Selector Record" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>UINT24</td><td>varSelector</td><td>Variation selector</td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>defaultUVSOffset</td><td>Offset to Default UVS Table. May be 0. </td><td class="auto-generated"> </td></tr><tr><td>ULONG</td><td>nonDefaultUVSOffset</td><td>Offset to Non-Default UVS Table. May be 0.</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>The Variation Selector Records are sorted in increasing
        order of 'varSelector'. No two records may have the same
        'varSelector'. All offsets in a record are relative to the
        beginning of the format 14 cmap subtable.</p><p>A Variation Selector Record and the data its offsets
        point to specify those UVSes supported by the font for which
        the variation selector is the 'varSelector' value of the
        record. The base characters of the UVSes are stored in the
        tables pointed to by the offsets. The UVSes are partitioned by
        whether they are default or non-default UVSes.</p><p>Glyph IDs to be used for non-default UVSes are specified
        in the Non-Default UVS table.</p><p>Default UVS Table</p><p>A Default UVS Table is simply a range-compressed list of
        Unicode scalar values, representing the base characters of the
        default UVSes which use the 'varSelector' of the associated
        Variation Selector Record.</p><div class="table"><a name="idm2347"></a><p class="title"><strong>Table 5.17. Default UVS Table header</strong></p><div class="table-contents"><table class="table" summary="Default UVS Table header" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>ULONG</td><td>numUnicodeValueRanges</td><td>Number of ranges that follow</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>This is immediately followed by 'numUnicodeValueRanges'
        Unicode Value Ranges, each of which represents a contiguous
        range of Unicode values.</p><div class="table"><a name="idm2361"></a><p class="title"><strong>Table 5.18. Unicode Value Range</strong></p><div class="table-contents"><table class="table" summary="Unicode Value Range" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>UINT24</td><td>startUnicodeValue</td><td>First value in this range</td><td class="auto-generated"> </td></tr><tr><td>BYTE</td><td>additionalCount</td><td>Number of <span class="emphasis"><em>additional</em></span>
            values in this range</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>For example, the range U+4E4D...U+4E4F (3 values) will
        set 'startUnicodeValue' to 0x004E4D and 'additionalCount' to
        2. A singleton range will set 'additionalCount' to 0.</p><p>('startUnicodeValue' + 'additionalCount') must not
        exceed 0xFFFFFF.</p><p>The Unicode Value Ranges are sorted in increasing order
        of 'startUnicodeValue'. The ranges must not overlap; i.e.,
        ('startUnicodeValue' + 'additionalCount') must be less than
        the 'startUnicodeValue' of the following range (if
        any).</p><p>Non-Default UVS Table</p><p>A Non-Default UVS Table is a list of pairs of Unicode
        scalar values and glyph IDs. The Unicode values represent the
        base characters of all non-default UVSes which use the
        'varSelector' of the associated Variation Selector Record, and
        the glyph IDs specify the glyph IDs to use for the
        UVSes.</p><div class="table"><a name="idm2384"></a><p class="title"><strong>Table 5.19. Non-Default UVS Table header</strong></p><div class="table-contents"><table class="table" summary="Non-Default UVS Table header" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>ULONG</td><td>numUVSMappings</td><td>Number of UVS Mappings that follow</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>This is immediately followed by 'numUVSMappings' UVS
        Mappings.</p><div class="table"><a name="idm2398"></a><p class="title"><strong>Table 5.20. UVS Mapping</strong></p><div class="table-contents"><table class="table" summary="UVS Mapping" border="1"><colgroup><col/><col/><col/><col/></colgroup><thead><tr><th>Type</th><th>Name</th><th>Description</th><td class="auto-generated"> </td></tr></thead><tbody><tr><td>UINT24</td><td>unicodeValue</td><td>Base Unicode value of the UVS</td><td class="auto-generated"> </td></tr><tr><td>USHORT</td><td>glyphID</td><td>Glyph ID of the UVS</td><td class="auto-generated"> </td></tr></tbody></table></div></div><br class="table-break"/><p>The UVS Mappings are sorted in increasing order of
        'unicodeValue'. No two mappings in this table may have the
        same 'unicodeValue' values.</p><p>Example</p><p>Here is an example of how a format 14 cmap subtable may
        be used in a font that is aware of JIS-2004 variant
        glyphs. The CIDs (character IDs) in this example refer to
        those in the Adobe Character Collection 'Adobe-Japan1', and
        may be assumed to be identical to the glyph IDs in the font in
        our example.</p><p>JIS-2004 changed the default glyph variants for some of
        its code points. For example:</p><p>JIS-90: U+82A6 -&gt; CID 1142</p><p>JIS-2004: U+82A6 -&gt; CID 7961</p><p>Both of these glyph variants are supported through the
        use of UVSes, as the following examples from Unicode's UVS
        registry show:</p><p>U+82A6 U+E0100 -&gt; CID 1142</p><p>U+82A6 U+E0101 -&gt; CID 7961</p><p>If the font wants to support the JIS-2004 variants by
        default, it will:</p><div class="itemizedlist"><ul class="itemizedlist" style="list-style-type: disc; "><li class="listitem"><p>encode glyph ID 7961 at U+82A6 in the Unicode cmap
            subtable,</p></li><li class="listitem"><p>specify &lt;U+82A6, U+E0101&gt; in the UVS cmap
            subtable's Default UVS Table ('varSelector' will be
            0x0E0101 and 'defaultUVSOffset' will point to data
            containing a 0x0082A6 Unicode value)</p></li><li class="listitem"><p>specify &lt;U+82A6, U+E0100&gt; -&gt; glyph ID 1142 in the
            UVS cmap subtable's Non-Default UVS Table ('varSelector'
            will be 0x0E0100 and 'nonDefaultBaseUVOffset' will point
            to data containing a 'unicodeValue' 0x82A6 and 'glyphID'
            1142). </p></li></ul></div><p>If, however, the font wants to support the JIS-90
        variants by default, it will:</p><div class="itemizedlist"><ul class="itemizedlist" style="list-style-type: disc; "><li class="listitem"><p>encode glyph ID 1142 at U+82A6 in the Unicode cmap
            subtable,</p><p>specify &lt;U+82A6, U+E0100&gt; in the
            UVS cmap subtable's Default UVS Table</p></li><li class="listitem"><p>specify &lt;U+82A6, U+E0101&gt; -&gt; glyph ID 7961 in the
            UVS cmap subtables Non-Default UVS Table </p></li></ul></div></div></div></div><div class="section"><div class="titlepage"><div><div><h3 class="title"><a name="section.6.4"></a>Mapping Process for Font Consumers</h3></div></div></div><div role="specification" class="section"><div class="titlepage"><div><div><h4 class="title"><a name="section.6.4.1"></a>Specification</h4></div></div></div><p>When a text is being shaped by a font consumer,
          character codes that are not mapped to any glyph in the font
          by the data in this table (either because there is no subtable for their encoding or
          or because the subtable in a format not supported by the
          application or because the subtable does not contain a mapping
          for this character code) XXX unknown format
          will be mapped to glyph index
          correspond to any glyph in the font should be mapped to
          glyph index 0. The glyph at this location must be a special
          glyph representing a missing character, commonly known as
          .notdef.</p></div></div><div role="discussion" class="section"><div class="titlepage"><div><div><h3 class="title"><a name="section.6.5"></a>Discussion</h3></div></div></div><p>
        In practice, font producers creating fonts with characters entirely
        within the Basic Multilingual Plane should generate <a class="link" href="chapter.cmap.html" title="Chapter 5. cmap - Character to Glyph Index Mapping Table">cmap</a>
        table entries with Unicode codepoint encoding using platform ID 0
        platform encoding ID 3, and platform ID 3 platform encoding 1. Character
        to glyph ID assignments compatible with the MacRoman encoding should be
        made using platform ID 1 platform encoding 0.
      </p><p>
        The choice of subtable format is not entirely a free one, as certain combinations of platform and platform encoding mandate particular
        formats:
      </p><div class="itemizedlist"><ul class="itemizedlist" style="list-style-type: disc; "><li class="listitem">
          When the platform ID is 0 and platform encoding is 5 (Unicode Variation Sequences), the subtable must be format 10.
        </li><li class="listitem">
          When platform ID is 3 and platform encoding ID is 1 (Windows Unicode),
          the subtable must be format 4.
        </li><li class="listitem">
          When the platform ID is 3 and platform encoding is 10 (Windows full-range
          Unicode) to access codepoints beyond the Basic Multilingual Plane,
          the subtable must be format 12.
        </li><li class="listitem">
          When the platform ID is 4 (Custom), the subtable must be format 0 or format 6.
        </li></ul></div><p>It is legal to have a single subtable which is referenced
          from multiple entries? This is useful when a given character
          encoding is present on multiple platforms. For example, if
          there is a Unicode cmap subtable, it can be referenced from
          one entry with platformID/encodingID (0, 3), and from
          another entry with (3, 1).</p><p>
          The language field   For example, a Mac OS Turkish
          <a class="link" href="chapter.cmap.html" title="Chapter 5. cmap - Character to Glyph Index Mapping Table">cmap</a> subtable must set this field to 18,
          since the Macintosh language ID for Turkish is 17. A Mac OS
          Roman <a class="link" href="chapter.cmap.html" title="Chapter 5. cmap - Character to Glyph Index Mapping Table">cmap</a> subtable must set this field
          to 0, since Mac OS Roman is not a language-specific
          encoding.</p></div><div role="fragment" class="section"><div class="titlepage"><div><div><h3 class="title"><a name="idm2458"></a>Various test fonts</h3></div></div></div></div></div>