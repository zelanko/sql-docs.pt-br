---
title: HierarchyID (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- hierarchyid
- hierarchyid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Hierarchy data type
- hierarchyid data type
ms.assetid: 69b756e0-a1df-45b3-8a24-6ded8658aefe
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 44299e7ddb90bdd52e2638dd859993513bd6f966
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="hierarchyid-data-type-method-reference"></a>referência de método do tipo de dados HierarchyID
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

O **hierarchyid** tipo de dados é um comprimento de variável de tipo de dados do sistema. Use **hierarchyid** representar posição em uma hierarquia. Uma coluna de tipo **hierarchyid** não representa automaticamente uma árvore. Depende do aplicativo gerar e atribuir valores **hierarchyid** de maneira que a relação desejada entre as linhas seja refletida nos valores.
  
Um valor do tipo de dados **hierarchyid** representa uma posição em uma hierarquia de árvore. Os valores para **hierarchyid** têm as seguintes propriedades:
  
-   Extremamente compacto  
     O número médio de bits necessários para representar um nó em uma árvore com *n* nós depende da média de fanout (o número médio de filhos de um nó). Para fanouts pequenos (0-7), o tamanho é de aproximadamente 6\*logA *n*  bits, onde A é o fanout médio. Um nó em uma hierarquia organizacional de 100.000 pessoas com um fanout médio de 6 níveis usa cerca de 38 bits. Isso é arredondado para 40 bits, ou 5 bytes, para armazenamento.  
-   A comparação está na ordem de profundidade  
     Dados dois valores de **hierarchyid** **a** r **b**, **a<b** significa que a vem antes de b em uma passagem de profundidade da árvore. Índices em tipos de dados **hierarchyid** estão na ordem de profundidade e os nós próximos uns dos outros em uma passagem de profundidade são armazenados próximos um ao outro. Por exemplo, os filhos de um registro são armazenados adjacentes àquele registro. Para obter mais informações, consulte [dados hierárquicos &#40; SQL Server &#41; ](../../relational-databases/hierarchical-data-sql-server.md).  
-   Suporte a inserções e exclusões arbitrárias  
     Usando o método [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) , é sempre possível gerar um irmão à direita de qualquer nó determinado, à esquerda de qualquer nó determinado ou entre dois irmãos. A propriedade de comparação é mantida quando um número arbitrário de nós é inserido ou excluído da hierarquia. A maioria das inserções e exclusões preserva a propriedade de densidade. Porém, inserções entre dois nós produzirão valores hierarchyid com uma representação ligeiramente menos compacta.  
-   A codificação usada no **hierarchyid** tipo é limitado a 892 bytes. Consequentemente, nós que têm muitos níveis em sua representação para se ajustarem a 892 bytes não podem ser representados pelo **hierarchyid** tipo.  
  
O **hierarchyid** tipo está disponível para clientes CLR como o **SqlHierarchyId** tipo de dados.
  
## <a name="remarks"></a>Comentários  
O **hierarchyid** tipo codifica informações logicamente sobre um único nó em uma árvore hierárquica codificando o caminho da raiz da árvore para o nó. Esse caminho é representado logicamente como uma sequência de rótulos de nós de todos os filhos visitados depois da raiz. Uma barra inicia a representação e um caminho que visita apenas a raiz é representado por uma barra única. Para níveis abaixo da raiz, cada rótulo é codificado como uma sequência de inteiros separados por pontos. A comparação entre filhos é executada comparando-se as sequências de inteiros separados por pontos na ordem alfabética. Cada nível é seguido por uma barra. Portanto, uma barra separa os pais de seus filhos. Por exemplo, a seguir é válida **hierarchyid** caminhos de comprimentos 1, 2, 2, 3 e 3 níveis respectivamente:
  
-   /  
  
-   /1/  
  
-   /0,3.-7/  
  
-   /1/3/  
  
-   /0.1/0.2/  
  
Podem ser inseridos nós em qualquer local. Nós inseridos depois **/1/2/** mas antes **/1/3/** pode ser representado como **/1/2.5/**. Nós inseridos antes de 0 têm a representação lógica como um número negativo. Por exemplo, um nó que vem antes de **/1/1/** pode ser representado como **/1/1 /**. Nós não podem ter zeros à esquerda. Por exemplo, **/1/1.1/** é válido, mas **/1/1.01/** não é válido. Para evitar erros, insira nós usando o [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) método.
  
## <a name="data-type-conversion"></a>Conversão de tipo de dados
O **hierarchyid** tipo de dados pode ser convertido em outros tipos de dados da seguinte maneira:
-   Use o [ToString ()](../../t-sql/data-types/tostring-database-engine.md) método para converter o **hierarchyid** valor para a representação lógica como um **nvarchar (4000)** tipo de dados.  
-   Use [ler ()](../../t-sql/data-types/read-database-engine.md) e [Write ()](../../t-sql/data-types/write-database-engine.md) converter **hierarchyid** para **varbinary**.  
-   Para transmitir **hierarchyid** parâmetros por meio de SOAP primeiro converta-os como cadeias de caracteres.  
  
## <a name="upgrading-databases"></a>Atualizando bancos de dados
Quando um banco de dados é atualizado para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o novo assembly e o **hierarchyid** tipo de dados será instalado automaticamente. Regras do supervisor de atualização detectam qualquer tipo de usuário ou assemblies com nomes conflitantes. O supervisor de atualização aconselhará renomear quaisquer assemblies conflitantes, bem como qualquer tipo de conflito, ou usar nomes de duas partes no código para fazer referência ao tipo de usuário preexistente.
  
Se uma atualização de banco de dados detectar um assembly de usuário com nome conflitante, ele o renomeará automaticamente e o colocará no banco de dados em modo de suspeição.
  
Se um tipo de usuário com nome conflitante existir durante a atualização, nenhuma etapa especial será efetuada. Depois da atualização, existirão ambos os tipos de usuário, antigo e novo. O tipo de usuário só estará disponível através de nomes de duas partes.
  
## <a name="using-hierarchyid-columns-in-replicated-tables"></a>Usando colunas hierarchyid em tabelas replicadas
Colunas do tipo **hierarchyid** pode ser usado em qualquer tabela replicada. Os requisitos para seu aplicativo dependem de a replicação ser unidirecional ou bidirecional e das versões de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizadas.
  
### <a name="one-directional-replication"></a>Replicação unidirecional
Replicação unidirecional inclui replicação de instantâneo, replicação transacional e replicação de mesclagem, nas quais não são feitas alterações no Assinante. Como **hierachyid** colunas trabalhar com uma replicação unidirecional depende da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o assinante está sendo executado.
-   Um [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Publisher pode replicar **hierachyid** colunas para um [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] assinante sem considerações especiais.  
-   Um [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] publicador deve converter **hierarchyid** colunas para replicá-las para um assinante que está executando [!INCLUDE[ssEW](../../includes/ssew-md.md)] ou uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssEW](../../includes/ssew-md.md)]e versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferecem suporte a **hierarchyid** colunas. Ainda que esteja usando uma dessas versões, você poderá replicar dados para um Assinante. Para tanto, você deve definir uma opção de esquema ou o nível de compatibilidade de publicação (para replicação de mesclagem) a que a coluna pode ser convertida para um tipo de dados compatível.  
  
Em ambos os cenários há suporte a filtragem de colunas. Isso inclui a filtragem **hierarchyid** colunas. Filtragem de linha tem suporte desde que o filtro não inclui um **hierarchyid** coluna.
  
### <a name="bi-directional-replication"></a>Replicação bidirecional
Replicação bidirecional inclui replicação transacional com assinaturas de atualização, replicação transacional ponto a ponto e replicação de mesclagem, nas quais não são feitas alterações no Assinante. A replicação permite que você configure uma tabela com **hierarchyid** colunas para replicação bidirecional. Observe os requisitos e considerações a seguir.
-   O Editor e todos os Assinantes devem estar executando [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
-   A replicação reproduz os dados como bytes e não executa nenhuma validação para assegurar a integridade da hierarquia.  
-   A hierarquia das alterações feitas na origem (Assinante ou Editor) não é mantida quando eles são replicados para o destino.  
-   Os valores de hash **hierarchyid** colunas são específicas para o banco de dados no qual eles são gerados. Portanto, o mesmo valor poderia ser gerado no Editor e Assinante, mas poderia ser aplicado a linhas diferentes. Replicação não verifica para essa condição, e não há nenhum modo interno de partição **hierarchyid** valores de coluna, como há para colunas de identidade. Os aplicativos devem usar restrições ou outros mecanismos para evitar tais conflitos não detectados.  
-   É possível que as linhas que se encontram inseridas no Assinante se tornem órfãs. A linha pai da linha inserida pode ter sido excluída no Editor. Isso resulta em um conflito não detectado quando a linha do Assinante é inserida no Editor.  
-   Filtros de coluna não é possível filtrar não anuláveis **hierarchyid** colunas: Inserções do assinante falharão, porque não há nenhum valor padrão para o **hierarchyid** coluna no publicador.  
-   Filtragem de linha tem suporte desde que o filtro não inclui um **hierarchyid** coluna.  
  
## <a name="see-also"></a>Consulte também
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[Referência de método de tipo de dados hierarchyid](http://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  

