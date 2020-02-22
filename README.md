# h264_qdct_ptc 

In the 1.2.20 version, we provide the practical H.264 video embedding and extraction tools, and associate codes for explaining PTC in practice. 
 
If you have any question, or find bugs, no hesitate to contact the author.
Author: Yu Wang. Email: wangyu9078@iie.ac.cn

Note: from 2020-2-20 to 2020-3-1, we will continually update.

(The project with full source codes will be posted upon the publication/accepted of our research).

<b> Publication </b><br/>
Minimizing Embedding Impact for H.264 Steganography by Progressive Trellis Coding
[Not be published]

<b> Files Explanation </b><br/>

--PTCodes (souce folder): contains all source codes. (Before research pulicaiton/accepted, we only provide a associate/necessary revised .c files, namely encoder_p.c, which includes ptrellis_coding, restore_context, x264_slice_write functions. If you are interested in the frame compression, look into the x264_slice_write function. If you are interested in coding contexts maintained, look into restore_context function. Last but not least, the progressive trellis coding process, that controls multiple coding contexts to expand paths, prune sub-optimal paths, match messages, and retrace short paths, is included in the ptrellis_coding function. Note that other necessary steps that dynamically generating multiple cover blocks/stego blocks, the block-by-block coding/modification manner and the organization of coder control, etc, are not shown yet.
Besides, more .c and .h files, such as x264.c/.h, macroblock_p.c/.h, common_p.c/.h, ratecontrol_p.c/.h, etc., are revised for the implementation of PTC.)
We will update this project and tell following video steganographic researchers how to compile the project on window/vs, how to modify the source codes to make steganographic modules integrated into video compression (that is a tough job). 

--embed.bat: contains a case of command line parameters, and double click it to run the embedding tool.

--extract.bat: contains a case of command line parameters, and double click it to run the extraction tool.

--video-decode.bat: contains a case of command line parameters, and double click it to run the H.264 decoder.

--PTC-s.exe: the embedding/encoding tool.

--ext-PTC.exe: the extraction/decoding tool.

--ldecode.exe: an ordinary H.264 decoder.

--meg.txt: a secret message file used for testing the tools. Users can 
modify messages inside arbitrarily.

--walk_cif_cover.264: This is a H.264 video for test, 376 frames, 30 fps, qp=28,  baseline, GOP=10, 352x288.

<b> Quick overview of usage </b><br/>
For embedding, first of all, we should decode 'walk_cif_cover.264' into raw YUV data file 'walk_cif_cover.yuv'. Next, compress it into a H.264 video stream 'walk_cif_stego.264' while embedding the 'meg.txt' using PTC-s.exe. 
For extraction, We decode the 'walk_cif_stego.264' into a YUV data file while extracting the messages into the file 'ext-meg.txt'.

=========================================

<b> 1.Compilation </b><br/>
<b> 2.Code explanation </b><br/>
<b> 3.command line parameters </b><br/>
<b> 4.Input/Output file format </b><br/>
<b> 5.Platform </b><br/>

=========================================

<b> 1.Compilation </b><br/>
Windows
MS Visual C++ 2013 or later

<b> 2.Code explanation </b><br/>
(waiting for updates recently)


<b> 3.command line parameters </b><br/>
3.1 Encoder/Embedding
Test case:
ptc-s.exe --fps 30 --profile baseline --level 3.0 --threads 1 --qp 28 --keyint 10 --input-res 352x288 --tune psnr --psnr --ssim --megfile meg.txt --tempfile 2temp.txt --seq 18 --pl 3 --embytes 0 -o walk_cif.264 walk_cif.yuv 

--fps frame per second
--qp quantization parameter
--keyint Gop size
--input-res width x height (resolution)
--megfile secret message file
--tempfile temp file
-o stegovideo (.264) covervideo (.yuv) 

3.2 Decoder/Extraction
Test case:
ldecod.exe -p InputFile=walk_cif.264 -p OutputFile=walk_dec.yuv -M ext-message.txt -T messagetemp.txt
-p InputFile=stego video 
-p OutputFile=decoded video
-M messages retrieved
-T temp file


<b> 4.Input/Output file format </b><br/>
For message embedding tool:
The source video material is read from raw YUV 4:2:0 data files.
The output is an h.264 video stream.

For message extraction tool:
The source video material is an h.264 video stream.
The output is raw YUV 4:2:0 data files..


<b> 5.Platform </b><br/>
(waiting for updates recently)





