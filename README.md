这个recipe是基于eesen代码改写的中文语音识别，语料库为清华语料库(data_thchs30)。
===
## 1 功能:
	1)可以实现中文语音识别  

	2)可以加入其它的汉语语料库进行算法研究
	
	3)也可以单独研究以wfst为架构的解码器，实现声学模型出来的音素到词的转换
	

## 2 算法:BiLSTM+CTC+WFST  

	1)BiLSTM:3 layers+ 1 projection layer,320 hidden units  

	2)CTC:216个声韵母标签+1个blank标签  

	3)WFST: CTC token fst(T.fst), lexicon fst(L.fst), language model fst(G.fst) 

## 3 实验结果:
	1)CTC训练标签正确率:92%左右  

	2)CTC交叉严重标签正确率:90%左右  

	3)最终的解码WER:25%左右  



## 4 该目录下的相关文件说明:  

	 1)运行该项目: ./run.sh 
			
		也可以单独运行每个高亮的shell脚本，其中  

		make_TLG_WFST.sh: 用来生成TLG.fst . 无需加参数运行,生成的文件所在的目录为:data/{train,test,dev,lang,search_Graph}.  

		feature.sh:用来生成wav音频数据的fbank特征，40+delta+double delta. 无需加参数运行,生成的文件所在目录为:data/{train,test,dev} ,fbank  

		train.sh: 训练声学模型 无需加参数运行，也可以修改该脚本里的网络参数。生成的文件所在目录为:exp/model_l$_c$  

		decode.sh:利用 声学模型 和集成了语言模型的WFST进行解码. 生成的文件所在目录为:exp/model_l$_c$/decode_test 


	2)数据准备:  

		准备语言模型languange model ,放入data/language_model目录下，语言模型的文件格式类似于清华的  

		准备字典lexicon.txt，放入 data/dict目录下  

		准备训练数据，放入corpus/train目录下，wav+text  

		准备测试数据，放入corpus/test目录下， wav+text  

		准备验证数据，放入corpus/dev目录下，wav+text  

## 5 安装eesen:
	1)要想运行该项目，必须根据https://github.com/srvk/eesen中的INSTALL安装eesen
