# MADR
A Matlab code for minimum absolute deviation distribution machine for regression.


%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%% exam   
clc    
close all    

addpath(genpath('MADR'))    

%% %%%------------------------kernel vMADR----------------------%%%    
load('X23.mat');    
    
%% [preY, mse, time]= vMADR_CD(testX, testY, trainX, trainY, [lambda1, lambda2, C, v, kerfPara], kerType);    
[preY1, mse1, time1]= vMADR_CD(testData, testLabel, trainData, trainLabel, [2^5, 2^5, 2^-4, 2^-8, 2^1], 'rbf');    
time1;    
    
    
%% %%%------------------------primal vMADR----------------------%%%    
load('MSDData.mat');    
    
%% model = vMADR_ASGD_train(trainY, sparse(trainX), [lambda1, lambda2, C, epsilon], '-s 1 -k 0');    
%% preY = vMADR_ASGD_predict(sparse(testX), sparse(trainX), model);    
%% trainX: each row represents an instance    
dataTrain = sparse(dataTrain);    
dataTest = sparse(dataTest);    
    
t1 = clock;    
model = vMADR_ASGD_train(targetTrain, dataTrain, [2^1, 2^3 2^9 2^9], '-s 1 -k 0');    
preY2= vMADR_ASGD_predict(dataTest, dataTrain, model);    
t2 = clock;   
time2 = etime(t2,t1);   
mse2 = sum(power(preY2 - targetTest, 2)) / length(targetTest);   
   
   
   
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%   
Dataset.   
Here we give the Baidu network disk link of the processed large-scale dataset MSD, if necessary, you can download it yourself.   
The link：https://pan.baidu.com/s/11BSDxwg0XX2f4cqDfbdKVQ    
Extraction code：isuk    
