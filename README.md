# antojs-audio
autojs录音功能,由java改写 java代码为:

importClass(java.io.File);
importClass(java.io.FilenameFilter);
importClass(java.io.IOException);
importClass(java.util.ArrayList);
importClass(java.util.HashMap);
importClass(java.util.List);
importClass(java.util.Map);

importClass(android.annotation.SuppressLint);
importClass(android.app.Activity);
importClass(android.app.AlertDialog);
importClass(android.content.DialogInterface);
importClass(android.content.DialogInterface.OnClickListener);
importClass(android.content.Intent);
importClass(android.media.MediaPlayer);
importClass(android.media.MediaRecorder);
importClass(android.net.Uri);
importClass(android.os.Bundle);
importClass(android.os.Environment);
importClass(android.os.Handler);
importClass(android.os.Message);
importClass(android.view.View);
importClass(android.widget.AdapterView);
importClass(android.widget.AdapterView.OnItemClickListener);
importClass(android.widget.AdapterView.OnItemLongClickListener);
importClass(android.widget.Button);
importClass(android.widget.ListView);
importClass(android.widget.SimpleAdapter);
importClass(android.widget.Toast);
importClass(java.text.ParseException);
importClass(java.text.SimpleDateFormat);
importPackage(java.util);
importClass(java.text.DecimalFormat);
var mRecAudioFile = "yp.mp3" ; // 录制的音频文件
var mRecAudioPath = "/storage/emulated/0/脚本/" ; // 录制的音频文件路徑
var mMediaRecorder;// MediaRecorder对象
var strTempFile = "recaudio_";// 零时文件的前缀
var mList;

runtime.requestPermissions(["android.permission.CAPTURE_AUDIO_OUTPUT"]);

function startRecord() {
    try {
        /* ①Initial：实例化MediaRecorder对象 */
        mMediaRecorder = new MediaRecorder();
        /* ②setAudioSource/setVedioSource */
        mMediaRecorder.setAudioSource(MediaRecorder.AudioSource.MIC);// 设置麦克风
        /*
         * ②设置输出文件的格式：THREE_GPP/MPEG-4/RAW_AMR/Default
         * THREE_GPP(3gp格式，H263视频
         * /ARM音频编码)、MPEG-4、RAW_AMR(只支持音频且音频编码要求为AMR_NB)
         */
        mMediaRecorder.setOutputFormat(MediaRecorder.OutputFormat.DEFAULT);
        /* ②设置音频文件的编码：AAC/AMR_NB/AMR_MB/Default */
        mMediaRecorder.setAudioEncoder(MediaRecorder.AudioEncoder.DEFAULT);
        /* ②设置输出文件的路径 */
        try {
            mRecAudioFile = File.createTempFile(strTempFile, ".amr",
                    mRecAudioPath);

        } catch (e) {
            toastLog(e);
        }
        mMediaRecorder.setOutputFile(mRecAudioPath+mRecAudioFile);
        /* ③准备 */
        mMediaRecorder.prepare();
        /* ④开始 */
        mMediaRecorder.start();
    } catch (e) {
        toastLog(e);
    }
}
function stopRecord() {
    if (mRecAudioFile != null) {
        /* ⑤停止录音 */
        mMediaRecorder.stop();
        /* 将录音文件添加到List中 */
        //addItem(mRecAudioFile);
        /* ⑥释放MediaRecorder */
        mMediaRecorder.release();
        mMediaRecorder = null;
    }
}

startRecord()
