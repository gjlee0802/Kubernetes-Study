# Kubernetes-Study
쿠버네티스 공부

## 강의 자료
https://www.youtube.com/watch?v=6n5obRKsCRQ&list=PLApuRlvrZKohaBHvXAOhUD-RxD0uQ3z0c

## 쿠버네티스 기본 설치
1. 도커 설치 및 컨테이너 런타임 설치   
https://kubernetes.io/ko/docs/setup/production-environment/container-runtimes/

2. kubeadm, kubelet, kubectl 설치   
https://kubernetes.io/ko/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

## 환경 구축 (VirtualBox 이용)
### 1. control-plane 환경   
~~~
$ sudo kuberadm init
~~~
이후 나오는 문구를 복사하여 다음 명령어 수행
~~~
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
~~~
가장 아래에 있는 출력 문구를 token.txt에 저장해두기.   
~~~
kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash>
~~~
### 2. worker-node 환경
다음과 같이 token.txt에 복사해둔 kubeadm join 명령을 이용하여 control-plane에 가입.   
~~~
# kubeadm join <control-plane-host>:<control-plane-port> --token <token> --discovery-token-ca-cert-hash sha256:<hash> --node-name <mynodename>
~~~
### 3. control-plane에서 노드 조회
![스크린샷, 2021-05-10 19-07-18](https://user-images.githubusercontent.com/49184890/117644726-c0209800-b1c4-11eb-8da6-383d92444c7d.png)
