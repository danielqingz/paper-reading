<i>Title</i>: <a href="https://link.springer.com/content/pdf/10.1007/s00330-015-3794-0.pdf">Free DICOM de-identification tools in clinical research functioning and safety of patient pravicy</a> (European Radiology 2015) <br>

<i>Author</i>: K.Y.E. Aryanto, M. Oudkerk, P.M.A. van Ooijen<br>
<i>Keywords</i>: DICOM Freeware Tools, Patient Data Privacy, Anoymisation and Pseudonymisation, Data Protection, Anonymous Testing

<i>Comments</i>: 

DICOM: Digital Imaging and Communications in Medicine

* Background


    在临床研究里为了保护被采集数据的患者隐私，一般要做de-identification来去除病人的 personal health information(PHI) or protected health information，人口统计信息（性别，年龄，种族，教育水平等），过往病史，用药记录，生化检查档案，精神状况检查等一些可以判断病人身份的信息。DICOM就是在医学图像里用来储存，交换这些信息的，包括图像信息+meta-data elements，但同时也可能使信息被泄露。
    一般有两种方式来de-identify，一种是匿名化（anonymization），把能够辨认出病人身份的信息替换成随机数据，只保留下辨认不出病人身份的数据；另一种是假名化（pseudonymization），用一些人工标识符来替换比较有识别性的信息，这样的话被授权的机构就可以去溯源信息，联系患者。
* Experimental setting

    - 工具：选择了十个免费的工具包
    - 数据：dummy DICOM image, 包括了header data和image pixels
    - 评判标准： 选了五十个data element来测试是否de-identify成功，50个一般是最低要求

* Results


    只有两个免费工具可以在default的情况下完成比较高的de-identify：CTP和DICOM Library，最后大概讨论了下免费工具的可用性一类的。
 * Discussion


    这边文章其实主要是看下前半部分，了解下DICOM文件的结构、用途和如何处理，包括一些处理标准参考，其实工具包选择方面一般是仁者见仁智者见智了。
  
  
  
  1/25/2023 Ziqian Huang
  
<br>

----

<br>

<i>Title</i>: <a href="https://arxiv.org/pdf/1710.09412.pdf">mixup: Beyond Empirical Risk Minimization</a> (European Radiology 2015) <br>

<i>Author</i>: Hongyi Zhang, Moustapha Cisse, Yann N. Dauphin, David Lopez-Paz<br>

<i>Comments</i>: 

01/25/2023 by Ziqian Huang
今天续上 uwu
