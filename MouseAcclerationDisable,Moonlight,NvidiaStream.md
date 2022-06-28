<!--
 * @Author       : Primimy
 * @Date         : 2022-06-28 11:55:54
-->
# Nvidia stream will automatically enable mouse acceleration when using moonlight to connect to the server.

# One way of fixing(not perfect)
1. Download a hex editor(Diskgeniuns, Notepad(with [HexEdit Plugin](https://github.com/chcg/NPP_HexEdit)), [Hextor](https://github.com/digitalw0lf/hextor))
2. Open the file(***C:\Program Files\NVIDIA Corporation\NvStreamSrv.exe***) in the hex editor.
3. Search the hex number(***FF 15 FF 60 0A 00***) and change it to (***B8 01 00 00 00 90***) from **0025D65B** to **0025D660**.(Tested on NvStreamSrv 7.1.3110.6651)
4. By the way, maybe there is still something incorrect with Nvidia Stream when you playing games using server mouse(espacially FPS or rhythm games), but now it's better than before.

# Reference
1. *https://github.com/moonlight-stream/moonlight-qt/issues/128*