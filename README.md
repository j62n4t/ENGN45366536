java c
ENGN4536/6536 - Wireless Communications
Simulink Project
GoalStudents are expected to use Matlab and Simulink as the tool to construct different wireless commu- nication systems based on lectures on fading channels, receiver diversity, and multi-carrier systems. Students are expected to apply the knowledge gained in this course to design the system parameters and analyse the performance. This is an individual project.
Assessment
•  Each student needs to submit a written report to present the project deliverables and answer the evaluation questions (Sections 1.3, 1.4, 2.3, 2.4, 3.3, 3.4, 4.3, and 4.4).  Students are able to use either the Simulink Project Report template, or write the report in a self-organising manner. Submit the report as a single PDF file and use the Simulink project coversheet as the front page.
•  In addition to the written report, each student needs to submit all the simulink files (Sections 1.2, 2.2, 3.2, and 4.2) in a single .zip file.
•  Thus, each student needs to submit two files (one PDF report with coversheet and one com- pressed file) in Wattle.  The submission is due at 11:55pm on 27 October 2024.  No late submission is accepted, unless an extension is granted by the course convenor.
•  This assessment is worth 20% of the total mark for undergraduate students.
•  This assessment is worth 18% of the total mark for postgraduate students.
Background and Important Information
•  Review Lectures delivered in Weeks 2–6 before starting doing the tasks, and pay particular attention to the contents on (i) wireless fading channels, (ii) modulation performance over wireless fading channels, (iii) receiver diversity, and (iv) orthogonal frequency division mul- tiplexing (OFDM).
•  There is one online lecture dedicated for the project, which will be made available in Wattle.
•  Project Coordinator and Tutor: Mr. Muhammad Usman (muhammad.usman@anu.edu.au).
Use of Matlab
•  There is no restriction on the version of Matlab used for this project.
•  Please indicate the version of Matlab used in the Simulink project coversheet.
•  Matlab access and support is available for everyone at ANU. Please refer to  https://au.mathworks.com/academia/tah-portal/australian-national-university-30869859.html
Total Mark: 100TASK I - QPSK over Flat Rayleigh Fading Channels                                      [18 Marks]
1.1 Theory [Lectures 4, 6, 8]
1.  Introduction to an ideal flat and fast Rayleigh fading channel model, i.e., independent and identically distributed (i.i.d.) Rayleigh fading channel.When modelling the wireless channel as an i.i.d. Rayleigh fading channel, the channel coef- ficient remains constant during a symbol period, but changes independently from one symbol period to another.  Effectively, we have Tc/Ts  =  1, where Tc is the channel coherence time and Ts is the symbol period. The channel coefficient h can be expressed/generated ash = hRe + ihIm ,                                                     (1)where hRe  and hIm  are independent random variables following the Gaussian distribution N(0, 2/1). Thus, the magnitude of h, denoted as |h|, follows the Rayleigh distribution, the probability density function (PDF) of which given byf(|h|) = 2|h|exp(−|h| 2 ).                                          (2)
Also, it is interesting to note that |h| 2 has a unit mean and follows the exponential distribution, the PDF of which given byf(|h| 2 ) = exp(−|h| 2 ).                                              (3)
In Task I, we use (1) to generate i.i.d. Rayleigh fading channel in Simulink.
2.  Using the simplified single-slope path loss model in [Lecture 4], the received signal power, Pr, is related to the transmit power, Pt, in linear scale given bywhere d0 is the reference distance,d is the distance between the transmitter and the receiver, η is the path loss component, and K is the parameter (in linear scale) related to antenna gains. Note that this is the large-scale effect of a channel, and we do not consider shadowing effects.3.  By jointly considering the large-scale path loss and small-scale fading, the received signal
(not power) is given bywhere x is the modulated symbol to be transmitted with normalised power (i.e., power equals one) and wis the additive white Gaussian noise (AWGN) at the receiver with power σ 2 . Thus, the signal-to-noise ratio (SNR), γ, at the receiver is written asγ =  .                                                  (6)
Because the mean value of |h| 2 is 1, the average SNR (which is averaged over different reali- sations of the fading channel coefficient) is denoted by γ and given byThe detection performance of a wireless communication system depends on the average SNR. For convenience, we normalise the signal power to 1. By keeping the same average SNR, we rewrite the received signal in (5) asy = hx + w′ ,                                                       (8)
where w′ is the equivalent AWGN with power For simplicity, in the Simulink project, we use the normalised symbol x (with power equals 1), and do NOT use power amplifier blocks to model the actual transmit power Pt. Hence, the effects of the transmit power and large-scale path loss are represented by setting the average SNR in the AWGN block.  Specifically, in the AWGN block, we choose mode as SNR, and then set SNR as the given value in the following lab procedure and set the input power as 1 watt.
4.  Coherent detection.  To detect/decode the transmitted symbol x from the received symbol y in (8), we need to first know the value of h.  Since h changes from one symbol period to another, the receiver needs to track its value continuously.  The process of tracking the channel coefficient is called channel estimation.  In practice, one cannot exactly track the channel coefficient in each symbol duration; thus there are always some errors in channel estimation.In the Simulink project, for simplicity, we assume that there is no channel estimation error, which means that the receiver always knows the channel coefficient correctly in each symbol period.For QPSK (or generally M-QAM) modulation, the coherent detection method uses the knowl- edge of channel coefficients by multiplying its conjugate with the received symbol. Thus, with both the received signal y in (8) and the channel coefficient h as the inputs of the coherent
detector, the output of the coherent detector is given by ˆ(x) asˆ(x) = h* hx + h*w′ = |h| 2x + h*w′ .                                      (9)Basically, coherent detection removes the phase distortion introduced by the wireless channel.
5.  The theoretical average bit error rate (BER) (or equivalently, bit error probability) expression for QPSK modulation over flat Rayleigh fading channels is given by(10)
In the high SNR regime where γ has a very large value, we approximate the average BER asP(¯)b  ≈  .                                                        (11)
1.2 Lab Procedure
1.  Build the system given in Fig.   1,  including  self-built i.i.d.   Rayleigh fading channel and coherent detection models. Name the file as QPSK   iid Rayleigh .slx.Note: Among those blocks in Fig.  1, some blocks are readily available in Matlab Simulink and some are not.  For example, the Bernoulli Binary Generator, Bit to Integer/Integer to Bit Converter, and QPSK Modulator/Demodulator Baseband are readily available in Mat- lab Simulink, but Rayleigh fading channel and the Coherent Detection block are not readily available. If a block is readily available in MatlabSimulink, please use it directly to construct 
Figure 1: Block diagram of Rayleigh fading channels and coherent detection.the wireless communication system. Otherwise, if a block is not readily available, please first construct a custom block using other readily available inbuilt blocks, and then use the custom block to construct the wireless communication system model.
2.  Set the parameters as
•  Sampling rate FS  = 106 Hz;
Note: The sample rate refers to the bitrate, i.e., Bernoulli binary generator rate.
•  Set the SNR mode in the AWGN block as SNR and set the SNR value from  0:2:30 dB. Please set one SNR value at one time.
Note: In some versions of Matlab, SNR can be set in terms of either Eb/No or Es/No. Please select Eb/No if applicable.
•  Simulation time Tend  = 0.01 s or higher;
Note: For larger SNR values where bit errors rarely happen, you may need to set Tend to a higher value to obtain non-zero bit error values.
3.  Run QPSK   iid Rayleigh .slx and record the BER for each SNR value.
1.3 Report Deliverables
1.  Present a BER v.s. SNR plot with BER values in log-scale and SNR from 0:2:30 in dB. In this plot, you should present two curves:  (i) the BER obtained from simulations in Simulink and (ii) the BER obtained using the theoretical expression in (10).  Use Matlab to compute the theoretical BER values and generate the plot. Please display (i) and (ii) in different ways, e.g., using solid lines to represent the theoretical BER and symbols to represent the simulated BER (such as the figure on Slide 6 in Lecture 8).                                                        [4 marks]
1.4 Evaluation Questions
1.  Explain in your own wordshow the self-built i.i.d. Rayleigh fading model works and the effect of each of the blocks included. Also explain how you choose the values of the parameters in each block in the system, such as the mean, variance, SNR, sample time, and power gain (which is a parameter in the block of power amplifier), if applicable.                        [5 marks]
2.  Explain in your own wordshow the self-built coherent channel detection model works and the effect of each of the blocks included.  Also, explain how you choose the values of the parameters in each block, such as the mean, variance, SNR, and power gain, if applicable.  [5 marks]
3.  Given a fixed SNR value/setting for the AWGN block, how would you set the equivalent Eb/N0代 写ENGN4536/6536 - Wireless Communications Simulink ProjectMatlab
代做程序编程语言 and Es/N0 ?                                        [4 marks]TASK II - QPSK over Flat Rayleigh Fading Channels with Receiver Diversity [25 Marks]
2.1 Theory [Lecture 10]
1.  Receiver diversity is a well-known technique to improve the reliability performance of wire- less communications in fading channels.   It takes advantage of the diversity of signals in different antennas at the receiver. There are several receiver diversity techniques, while in this task, we only consider two of them: Selection combining (SC) and maximum ratio combining (MRC).
We now assume that the receiver is equipped with two receive antennas.  In this case, the received signals at the two antennas are given by
y1 [t] = h1 [t]x[t] + w1 [t],                                          (12)
and
y2 [t] = h2 [t]x[t] + w2 [t].                                          (13)
We assume both noises w1 [t] and w2 [t] are AWGN with the same variance.For SC, during each symbol period, we simply choose the signal (or effectively the antenna) that experiences the channel with the best fading condition to do coherent detection. That is, the indexof the signal or antenna to be chosen is
arg i |hi| 2 .                                                (14)
For MRC, we smartly combine the signals received at the two antennas as 

2.  For SC with M antennas, the PDF of the post-processing SNR, γΣ , can be written as

where γ is the average pre-processing SNR of the received signal at a single antenna. For MRC with M antennas, the PDF of post-processing SNR, γΣ , can be written as

Let us denote Pb(γ) as the BER for a certain modulation scheme with a certain SNR γ . The average BER, denoted as Pb, can be calculated by
(18)
For QPSK, we have
Pb(γ) = Q(√γ ) .                                                 (19)
Thus, the average BER for QPSK with SC/MRC can be calculated by solving the integral in
(18).
Figure 2: Block diagram of SC.
Figure 3: Block diagram of MRC.
2.2 Lab Procedure
•  Build the system given in Fig. 2, including self-built i.i.d. Rayleigh fading channel and selec- tion diversity (SD) detection models. Name the file as QPSK Rayleigh   SIMO   SC .slx.
•  Set the parameters as
–  Sample rate FS  = 106 Hz;
–  Simulation time Tend  = 0.1 s or higher;
–  Set the SNR mode in all the AWGN blocks as SNR and set the SNR value from 0:2:30 dB.
•  Run QPSK Rayleigh   SIMO   SC .slx and record the BER for each SNR value.
•  Build the system given in Fig. 3, including self-built i.i.d. Rayleigh fading channel and MRC detection models, as QPSK Rayleigh   SIMO MRC .slx.
•  Set the parameters as in the previous step.
•  Run QPSK Rayleigh   SIMO MRC .slx and record the BER for each SNR value.
2.3 Report Deliverables1.  Present the block diagrams of SC and MRC detection models.                                  [8 marks]
2.  Present a BER v.s. SNR plot with BER values in log-scale and SNR from 0:2:30 in dB. In this plot, you should present four curves: (i) the BER obtained from simulations in Simulink for both SC and MRC and (ii) the BER obtained using the theoretical expressions for both SC and MRC. Use Matlab to compute the theoretical BER values and to generate the plot. Please display (i) and (ii) in different ways.           [4 marks]
2.4 Evaluation Questions1.  Explain in your own words how the self-built SC and MRC models work and the effect of each of the blocks included.  Also explain how you choose the values of the parameters in each block in SC and MRC, such as the mean, variance, SNR, and power gain, if applicable.
[6 marks]
2.  Compare the BER-SNR curves for the system deploying receiver diversity techniques in Sec- tion 2.3.2 with the BER-SNR curves in Task I. Describe your observation and explain why receive diversity can improve the reliability performance.       [2 marks]
3.  Explain in your own words why MRC outperforms SC. Despite such a performance gain, what is the disadvantage (or cost) of MRC relative to SC?                                         [2 marks]
4.  Do you think i.i.d. Rayleigh fading channel really happens in practice? If not, what would be a better model?             [3 marks]TASK III - Differential QPSK over Multi-path Rayleigh Fading Channels [21 Marks]
3.1 Theory [Lecture 7]
1.  Differential modulation.In Task I, we have learned coherent detection which relies on channel estimation. However, due to the difficulties as well as the cost and complexity associated with channel estimation, differential modulation techniques, which do not require channel estimation, are often used in practical communication systems.The basic principle of differential modulation is to use the previous symbol as a phase ref- erence for the current symbol, thus avoiding the need for a coherent phase reference at the receiver. Specifically, the information bits are encoded as the difference in phase between the current symbol and the previous symbol.
At symbol time t, we assume that the input symbol after QPSK or PSK modulation is d[t], and the output symbol after differential encoding isx[t] = d[t]x[t − 1],                                                 (20)
where x[t − 1] is the output symbol at time t − 1, as shown in Fig. 4.
For this differential encoder, the output symbol is effectively obtained by accumulating the phase and modifying the amplitude of the previous symbol as
After x[t] passes through the wireless channel with channel coefficient h[t], the received signal can be written asy[t] = h[t]x[t] + w[t],                                              (23)
where w[t] is the AWGN at the receiver.
For the differential decoder, as shown in Fig. 5, let us denote the detected symbol by d(ˆ)[k] and express it asd(ˆ)[t] =  =  ≈  = d[t].             (24)
Therefore, in order to make the estimation/approximation with high accuracy, two conditions should be satisfied simultaneously when we use differential coding/decoding. They are:
Figure 4: Differential encoder.
Figure 5: Differential decoder.
Figure 6: Block diagram of QPSK with differential encoding/decoding.
(a)  The channel coefficient takes nearly the same value in two consecutive symbol periods, i.e., h[t] ≈ h[t − 1], and
(b)  High SNR regime,i.e.,  ≫ 1.
2.  In the high SNR regime, the theoretical average BER expressions for conventional and differ- ential QPSK over flat Rayleigh fading channel are given byPSK  =                                                      (25)
andiff-QPSK  =                                                    (26)
respectively.
3.2 Lab Procedure
•  Build the system given in Fig.  6, using a multi-path Rayleigh fading channel model in the Simulink library and self-built differential encoding/decoding model.
Name the file as QPSK Rayleigh differential   coding .slx.
•  Scenario 1: Set the parameters as
–  Sample rate FS  = 106 Hz;
–  Simulation time Tend  = 1 s or higher;
–  For the multi-path Rayleigh channel block, set the Doppler spectrum type as “flat” and set Doppler shift as Ds  = 100 Hz;
–  For the multi-path Rayleigh channel block, set path delay as [0] and set path gain as [0] dB;
–  Set the SNR mode in the AWGN block as SNR and set the SNR value from  0:2:30 dB.
•  Run QPSK Rayleigh differential   coding .slx and record the BER for each SNR value.
•  Scenario 2: Set the parameters as
–  For the multi-path Rayleigh channel block, set Doppler shift as Ds  = 100 Hz;
–  For the multi-path Rayleigh channel block, set path delay as  [0,1 . 8e-5] and set path gain as  [0,3] dB;
–  Set the SNR mode in the AWGN block as SNR and set the SNR value from  0:2:30 dB.
•  Run QPSK Rayleigh differential   coding .slx and record the BER for each SNR value.
•  Scenario 3: Set the parameters as
–  For the multi-path Rayleigh channel, Doppler shift Ds takes values from [100  1000  5000  10000  15000  20000  25000  30000] Hz;
–  For the multi-path Rayleigh channel block, set path delay as [0] and set path gain as [0] dB;
–  Set the SNR mode in the AWGN block as SNR and set SNR as (10 + κ) dB, where κ is the last digit of your Uni ID. For example, if your Uni ID is u1234567, the SNR in this
scenario is set as 17 dB.
•  Run QPSK Rayleigh differential   coding .slx and record the BER for each Doppler shift value.
3.3 Report Deliverables
1.  Present a BER v.s. SNR plot with BER values in log-scale and SNR from 0:2:30 in dB. In this plot, you should have two curves:  (i) the BER obtained from simulations for Scenario 1 and (ii) the BER obtained from simulations for Scenario 2. The difference between the two curves shows the effect of different delay spread.                   [3 marks]
2.  Present a BER v.s. Doppler shift plot with BER values in log-scale, using the results obtained from simulations for Scenario 3.         [3 marks]
3.4 Evaluation Questions
1.  Explain in your own words how the self-built differential encoding/decoding model works and the effect of each of the blocks included.  Also, explain how you choose the values of the parameters in each block in the differential encoding/decoding block, such as delay, and power gain, if applicable.              [6 marks]
2.  Can you explain why the first symbol is often detected in error, even in slow fading channels in the high SNR regime?                   [3 marks] (Hint: Think about differential encoding/decoding.)
3.  Compare the BER plots obtained from simulations for Scenarios 1 and 2 with the BER plot obtained in Task I. Describe your observation and explain why the performance with differ- ential coding is better/worse than that with coherent detection?     [3 marks]
4.  Using the criteria we have learned in [Lecture 7] to determine the range of Doppler shift, Ds , for fast, medium-rate, and slow fading channel.                                                          [3 marks]
         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
