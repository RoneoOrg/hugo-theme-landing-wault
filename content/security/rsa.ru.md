---
title: "RSA"
aux: "Алгоритм RSA (Rivest-Shamir-Adleman) является основой криптосистемы, который обеспечивает шифрование 
с открытым ключом и широко используется для защиты конфиденциальных данных, особенно когда он отправляется 
по небезопасной сети, такой как Интернет."
---

Криптография с открытым ключом, также известная как асимметричная криптография, использует два разных, 
но математически связанных ключа — один открытый и один закрытый. Открытый ключ может быть передан всем, 
тогда как закрытый ключ должен храниться в секрете.

В криптографии RSA как открытый, так и закрытый ключи могут шифровать сообщение. Ключ, противоположный 
тому, который используется для шифрования сообщения, используется для его расшифровки. Этот атрибут является 
одной из причин, по которой RSA стал наиболее широко используемым асимметричным алгоритмом: он обеспечивает 
конфиденциальность, целостность и подлинность электронных коммуникаций и хранения данных.

Многие протоколы, включая SSH, OpenPGP, S/MIME и SSL/TLS, полагаются на RSA для функций шифрования и 
цифровой подписи. Он также используется в программном обеспечении — браузеры являются очевидным примером, 
так как им необходимо установить безопасное соединение через небезопасную сеть, такую как Интернет.

## Реализация RSA

Wault использует RSA с 4096-битным ключем в режиме OAEP[^1]. При регистрации нового пользователя, Wault
генерирует пару ключей RSA используя криптографический генератор случайных чисел. При создании воркспейса,
генерируется ключ [блочного]({{< relref "/security/aes" >}}) шифрования, которым будут зашифрованны все данные внутри 
воркспейса. При этом сам блочный ключ шифруется публичным ключем пользователя. Данный подход  позволяют
одному пользователю создавать множество воркспейсов, а также делиться доступом к своим воркспейсам
другим пользователям, зарегистрированным в Wault.

[^1]: [Оптимальное асимметричное шифрование с дополнением](https://ru.wikipedia.org/wiki/Оптимальное_асимметричное_шифрование_с_дополнением)