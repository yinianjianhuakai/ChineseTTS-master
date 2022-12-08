# TTSChinese
<p align="center">
    <a href="https://github.com/tensorspeech/TensorFlowTTS/actions">
        <img alt="Build" src="https://github.com/tensorspeech/TensorFlowTTS/workflows/CI/badge.svg?branch=master">
    </a>
    <a href="https://github.com/tensorspeech/TensorFlowTTS/blob/master/LICENSE">
        <img alt="GitHub" src="https://img.shields.io/github/license/tensorspeech/TensorflowTTS?color=red">
    </a>
    <a href="https://colab.research.google.com/drive/1akxtrLZHKuMiQup00tzO2olCaN-y3KiD?usp=sharing">
        <img alt="Colab" src="https://colab.research.google.com/assets/colab-badge.svg">
    </a>
</p>

这是一个TensorFlowTTS中文语音合成的Android demo工程。项目基于TensorFlowTTS的[Android example](https://github.com/TensorSpeech/TensorFlowTTS/tree/master/examples/android)。在此基础上做了些修改，并且针对数字的播报做了简单的转换和处理。
### 相关参考
- 生成tflite文件，具体可参考此[colab](https://colab.research.google.com/drive/1Ma3MIcSdLsOxqOKcN1MlElncYMhrOg3J?usp=sharing#scrollTo=KCm6Oj7iLlu5)进行。在转换成tflite时建议大家安装最新版本的tensorflow，否则可能会导致转换后的模型在安卓手机上跑时会出现杂音的情况。
- 修改原demo项目中的部分代码参数，具体可参考博客[TensorflowTTS 中文android客户端](https://blog.csdn.net/ss182172633/article/details/109851660)。最关键的中文text2ids的Processor博客中没有给出，根据参考baker_mapper.json自己写了一个，汉字转拼音用的是pinyin4j的工具库，然后对照着colab上的结果进行拼接，后续计划继续完善转换播报的规则代码，例如2021/02/07的格式转换成日期的播报方式，也希望大家可以一起补充完善。

## 使用

### 添加依赖
```gradle
allprojects {
  repositories {
    ...
    maven { url 'https://jitpack.io' }
  }
}

  dependencies {
	        dependencies {
            	       implementation 'com.github.jinguangyang:ChineseTTS:1.0.0'
            	}
}

```


### 初始化
```init
 TtsManager.getInstance().init(this);

        TtsStateDispatcher.getInstance().addListener(new OnTtsStateListener() {
            @Override
            public void onTtsReady() {
                speakBtn.setEnabled(true);
            }

            @Override
            public void onTtsStart(String text) {
            }

            @Override
            public void onTtsStop() {
            }
        });
```



### 开始语音

```speak
  TtsManager.getInstance().speak(inputText, speed, true);
```



### 结束语音



```stop
    TtsManager.getInstance().stopTts());
```


目前不支持按时间格式进行播报，有兴趣的大神可以完善



# ChineseTTS-master
