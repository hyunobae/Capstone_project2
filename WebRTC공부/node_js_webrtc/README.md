# Node.JS�� signaling server ���� �� webRTC ���

���� ����Ʈ : https://forest71.tistory.com/211

## ����� & ����

���ۿ� �ռ� Node.js�� ��ġ�Ǿ� �־���Ѵ�.

���� �� ������������ `cmd`â�� ��� `npm i` �Է��ؼ� ���࿡ �ʿ��� ���̺귯������ ��ġ�Ѵ�.

�� ��, `node index.js`�� �Է��Ͽ� �� ���� ����.

���� SSL�� ������ ������ ī�޶�(webRTC)�� �̿��� �� �����Ƿ� NodeJS�� SSL�� �����ϱ� ���� SSL�� ����.
> ���� ����꿡�� Ȥ�ø��� private.pem�� public.pem�� �÷����� �ʾ����� �Ʒ� ����Ʈ�����ؼ� ����� ��.<br>
> https://blog.naver.com/PostView.nhn?blogId=baekmg1988&logNo=221454486746 <br>
> �׸��� �Ʒ��� ���� �Է�<Br>
> `openssl genrsa 1024 > private.pem`  => OpenSSL�� ����Ű ���� ����   <br>   
> `openssl req -x509 -new -key private.pem > public.pem`  => ����Ű�� ���� �Ǵ� ����Ű ����<br>

�� ���ϵ��� `index.js`�� ���� ������ �־��.

�� ���� ���� �������� `cmd`��� `node index.js` �Է��ؼ� �� ���� ����.

�׸��� `https:{ip�ּ�}:3000`���� pc�� �޴������� �����ϸ� �Ʒ��� ���� �� �� ī�޶� ȭ���� ���δ�.<br>

![webRTC2](./webRTC2.jpg)