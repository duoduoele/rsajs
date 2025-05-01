```
import rsajs from 'https://deno.land/x/rsajs@v1.0.0/rsajs.js';

// 生成RSA密钥对
let rsa = new rsajs(); // 可以指定密钥长度，默认为1024位
// let rsa = new JSEncrypt({ default_key_size: 2048 }); // 密钥长度为2048,速度稍慢
let publicKey = rsa.getPublicKey(); // 获取公钥
let privateKey = rsa.getPrivateKey(); // 获取私钥
console.log("Public Key: " + publicKey);
console.log("Private Key: " + privateKey);


function rsa_encrypt(text) {
	rsa.setPublicKey(publicKey);
	return rsa.encrypt(text);
};
let encrypt_data = rsa_encrypt('text')
console.log(encrypt_data);

function rsa_decrypt(text) {
	rsa.setPrivateKey(privateKey);
	return rsa.decrypt(text);
};
let decrypt_data = rsa_decrypt(encrypt_data);
console.log(decrypt_data);

// ---------------------------------------------------

import CryptoJS from 'https://deno.land/x/cryptojs@v1.0.8/cryptojs.js';

function rsa_sign(text) {
	rsa.setPrivateKey(privateKey);
	return rsa.sign(text,CryptoJS.SHA256,'sha256')
};
let signature = rsa_sign('text')
console.log(signature);

function rsa_sign_verify(text) {
	rsa.setPublicKey(publicKey);
	return rsa.verify('text', signature, CryptoJS.SHA256);
};
console.log(rsa_sign_verify(signature))
```
