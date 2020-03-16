### Diferenças entre bancos de dados relacionais e não-relacionais

Bancos de dados relacionais contém dados estruturados e relacionados entre si por identificadores. São caracterizados por manter um padrão (modelo) de dados, além de possuir conceitos comuns como restrições, contraints, normalização, chaves primárias e chaves estrangeiras. Tem como linguagem padrão o SQL (ainda que não seja a única).

Operações em bancos relacionais são baseadas nas propriedades ACID (atomicidade, consistencia, isolamento e durabilidade). Todos os comandos de uma operação devem ser refletidos na base de dados e cada um deve manter a integridade dos dados em termos de relacionamentos, unicidade e restrições, do contrário não há alterações no banco. 

Operações são isoladas e por isso uma instrução não influencia o resultado de outra mesmo que ocorra no mesmo instante. Porém, se um usuário tenta atualizar o modelo ou um campo que esteja sendo utilizado por outro usuário a operação não é realizada porque viola a integridade dos dados. 

O modelo relacional é útil para bases que fazem relação entre clientes e pagamentos, por exemplo, cujos dados escalam na vertical. Porém, não serve a modelos de negocios cujos dados escalam horizontalmente e crescem exponencialmente como redes sociais. 

Os modelos não relacionais, por outro lado, podem manter a consistencia e permitir particionar os dados em diferentes componentes de um cluster. Neste modelo, os objetos são independentes (são denominados documentos) e não obedecem a um esquema ou modelo predeterminado. Cada registro é, portanto, independente, o que torna possivel copiar um conjunto de dados para outros servidores e adicionar novos campos sem comprometer a integridade.

Nem todos as propriedades, no entanto, podem ser mantidas. Manter alta disponibilidade e particionamento significa normalmente abrir mão de consistência porque os dados precisam ser mais independentes, e manter alta disponibilidade e consistencia significa ter dados menos particionados para garantir integridade.


