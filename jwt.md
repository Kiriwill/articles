### Tokens JWT utilizam criptografia assimétrica para garantir segurança e integridade. Como eles facilitam e/ou dificultam o processo de autenticação de usuários?

JWT é um padrão de segurança que utiliza o formato JSON para formar tokens compactos e transmitir informações. Ele consiste em três partes separadas por pontos e codificadas: header, payload e signature. Eles são compactos e quase todas as linguagens contém parsers para ler e escrever em formato JSON.

Tokens JWT são credenciais que garantem a segurança e autenticidade de quem o requisita. Para garantir a segurança é necessário, entretanto, que os tokens contenham um tempo de expiração determinado e definido entre as partes.  Por possuírem informações confidenciais é importante que não sejam armazenados no cache do Browser ou em cookies. 

Quando gerados a partir de algoritmos HMAC SHA256, os tokens podem ser decodificados e por isso o payload do mesmo não deve conter informações secretas. Em caso de utilização de autorização HSA, chaves privadas devem ser armazenadas em local seguro e preferencialmente com controle de acesso.

Quando utilizados com protocolo OAuth a criação do token torna o processo de autorização longo. Exige-se que o usuário passe por autorização manual de certificação de seu login e senha para então obter o acesso. Isso pode provocar a evasão do usuário antes que o processo seja completado.
