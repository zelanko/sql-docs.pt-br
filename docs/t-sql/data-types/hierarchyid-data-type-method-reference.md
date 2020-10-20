---
description: referência de método do tipo de dados hierarchyid
title: hierarchyid (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e9968e1537901de729406c5b0ddc21857e74b886
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037484"
---
# <a name="hierarchyid-data-type-method-reference"></a>referência de método do tipo de dados hierarchyid
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

O tipo de dados **hierarchyid** é um tipo de dados do sistema de tamanho variável. Use **hierarchyid** para representar posição em uma hierarquia. Uma coluna de tipo **hierarchyid** não representa automaticamente uma árvore. Depende do aplicativo gerar e atribuir valores **hierarchyid** de maneira que a relação desejada entre as linhas seja refletida nos valores.
  
Um valor do tipo de dados **hierarchyid** representa uma posição em uma hierarquia de árvore. Os valores para **hierarchyid** têm as seguintes propriedades:
  
-   Extremamente compacto  
     O número médio de bits necessários para representar um nó em uma árvore com *n* nós depende da média de fanout (o número médio de filhos de um nó). Para fanouts pequenos (0-7), o tamanho é de aproximadamente 6\*logA*n* bits, em que A é o fanout médio. Um nó em uma hierarquia organizacional de 100.000 pessoas com um fanout médio de 6 níveis usa cerca de 38 bits. Isso é arredondado para 40 bits, ou 5 bytes, para armazenamento.  
-   A comparação está na ordem de profundidade  
     Dados dois valores de **hierarchyid****a** r **b**, **a<b** significa que a vem antes de b em uma passagem de profundidade da árvore. Índices em tipos de dados **hierarchyid** estão na ordem de profundidade e os nós próximos uns dos outros em uma passagem de profundidade são armazenados próximos um ao outro. Por exemplo, os filhos de um registro são armazenados adjacentes àquele registro. Para obter mais informações, consulte [Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md).  
-   Suporte a inserções e exclusões arbitrárias  
     Usando o método [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md) , é sempre possível gerar um irmão à direita de qualquer nó determinado, à esquerda de qualquer nó determinado ou entre dois irmãos. A propriedade de comparação é mantida quando um número arbitrário de nós é inserido ou excluído da hierarquia. A maioria das inserções e exclusões preserva a propriedade de densidade. Porém, inserções entre dois nós produzirão valores hierarchyid com uma representação ligeiramente menos compacta.  
-   A codificação usada no tipo **hierarchyid** está limitada a 892 bytes. Por conseguinte, os nós que têm muitos níveis em sua representação para se ajustarem a 892 bytes não podem ser representados pelo tipo **hierarchyid**.  
  
O tipo **hierarchyid** está disponível para clientes CLR como o tipo de dados **SqlHierarchyId**.
  
## <a name="remarks"></a>Comentários  
O tipo **hierarchyid** logicamente codifica informações sobre um único nó em uma árvore hierárquica codificando o caminho da raiz da árvore ao nó. Esse caminho é representado logicamente como uma sequência de rótulos de nós de todos os filhos visitados depois da raiz. Uma barra inicia a representação e um caminho que visita apenas a raiz é representado por uma barra única. Para níveis abaixo da raiz, cada rótulo é codificado como uma sequência de inteiros separados por pontos. A comparação entre filhos é executada comparando-se as sequências de inteiros separados por pontos na ordem alfabética. Cada nível é seguido por uma barra. Portanto, uma barra separa os pais de seus filhos. Por exemplo, são caminhos de **hierarchyid** válidos, respectivamente, de tamanhos 1, 2, 2, 3 e 3 níveis:
  
-   /  
  
-   /1/  
  
-   /0,3.-7/  
  
-   /1/3/  
  
-   /0.1/0.2/  
  
Podem ser inseridos nós em qualquer local. Nós inseridos após **/1/2/**, mas antes de **/1/3/**, podem ser representados como **/1/2.5/**. Nós inseridos antes de 0 têm a representação lógica como um número negativo. Por exemplo, um nó que vem antes de **/1/1/** pode ser representado como **/1/-1/**. Nós não podem ter zeros à esquerda. Por exemplo, **/1/1.1/** é válido, mas **/1/1.01/** não é válido. Para evitar erros, insira nós usando o método [GetDescendant](../../t-sql/data-types/getdescendant-database-engine.md).
  
## <a name="data-type-conversion"></a>Conversão de tipo de dados
O tipo de dados **hierarchyid** pode ser convertido em outros tipos de dados, da seguinte maneira:
-   Use o método [ToString()](../../t-sql/data-types/tostring-database-engine.md) para converter o valor de **hierarchyid** na representação lógica como um tipo de dados **nvarchar(4000)**.  
-   Use [Read ()](../../t-sql/data-types/read-database-engine.md) e [Write ()](../../t-sql/data-types/write-database-engine.md) para converter **hierarchyid** em **varbinary**.  
-   Para transmitir parâmetros de **hierarchyid** por SOAP, primeiro converta-os em cadeias de caracteres.  
  
## <a name="upgrading-databases"></a>Atualizando bancos de dados
Quando um banco de dados for atualizado para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], os novo assembly e o tipo de dados **hierarchyid** serão instalados automaticamente. Regras do supervisor de atualização detectam qualquer tipo de usuário ou assemblies com nomes conflitantes. O supervisor de atualização aconselhará renomear quaisquer assemblies conflitantes, bem como qualquer tipo de conflito, ou usar nomes de duas partes no código para fazer referência ao tipo de usuário preexistente.
  
Se uma atualização de banco de dados detectar um assembly de usuário com nome conflitante, ele o renomeará automaticamente e o colocará no banco de dados em modo de suspeição.
  
Se um tipo de usuário com nome conflitante existir durante a atualização, nenhuma etapa especial será efetuada. Depois da atualização, existirão ambos os tipos de usuário, antigo e novo. O tipo de usuário só estará disponível através de nomes de duas partes.
  
## <a name="using-hierarchyid-columns-in-replicated-tables"></a>Usando colunas hierarchyid em tabelas replicadas
Podem ser usadas colunas do tipo **hierarchyid** em qualquer tabela replicada. Os requisitos para seu aplicativo dependem de a replicação ser unidirecional ou bidirecional e das versões de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizadas.
  
### <a name="one-directional-replication"></a>Replicação unidirecional
Replicação unidirecional inclui replicação de instantâneo, replicação transacional e replicação de mesclagem, nas quais não são feitas alterações no Assinante. O modo de funcionamento das colunas **hierachyid** com a replicação unidirecional depende da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executada pelo Assinante.
-   Um Editor do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] pode replicar colunas **hierachyid** para um Assinante do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sem considerações especiais.  
-   Um Publicador do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] deve converter colunas **hierarchyid** para replicá-las para um Assinante que executa o [!INCLUDE[ssEW](../../includes/ssew-md.md)] ou uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssEW](../../includes/ssew-md.md)] e versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dão suporte às colunas **hierarchyid**. Ainda que esteja usando uma dessas versões, você poderá replicar dados para um Assinante. Para tanto, você deve definir uma opção de esquema ou o nível de compatibilidade de publicação (para replicação de mesclagem) a que a coluna pode ser convertida para um tipo de dados compatível.  
  
Em ambos os cenários há suporte a filtragem de colunas. Isso inclui a filtragem de colunas **hierarchyid**. Há suporte para a filtragem de linha, desde que o filtro não inclua uma coluna **hierarchyid**.
  
### <a name="bi-directional-replication"></a>Replicação bidirecional
Replicação bidirecional inclui replicação transacional com assinaturas de atualização, replicação transacional ponto a ponto e replicação de mesclagem, nas quais não são feitas alterações no Assinante. A replicação permite configurar uma tabela com colunas **hierarchyid** para replicação bidirecional. Observe os requisitos e considerações a seguir.
-   O Editor e todos os Assinantes devem estar executando [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
-   A replicação reproduz os dados como bytes e não executa nenhuma validação para assegurar a integridade da hierarquia.  
-   A hierarquia das alterações feitas na origem (Assinante ou Editor) não é mantida quando eles são replicados para o destino.  
-   Os valores de hash das colunas **hierarchyid** são específicos ao banco de dados no qual eles são gerados. Portanto, o mesmo valor poderia ser gerado no Editor e Assinante, mas poderia ser aplicado a linhas diferentes. A replicação não verifica se existe essa condição e não há nenhum modo interno de particionar valores da coluna **hierarchyid**, ao contrário das colunas IDENTITY. Os aplicativos devem usar restrições ou outros mecanismos para evitar tais conflitos não detectados.  
-   É possível que as linhas que se encontram inseridas no Assinante se tornem órfãs. A linha pai da linha inserida pode ter sido excluída no Editor. Isso resulta em um conflito não detectado quando a linha do Assinante é inserida no Editor.  
-   Filtros de colunas não podem filtrar colunas **hierarchyid** que não permitem valor nulo: as inserções do Assinante falharão, porque não há nenhum valor padrão para a coluna **hierarchyid** no Publicador.  
-   Há suporte para a filtragem de linha, desde que o filtro não inclua uma coluna **hierarchyid**.  
  
## <a name="see-also"></a>Veja também
[Dados hierárquicos &#40;SQL Server&#41;](../../relational-databases/hierarchical-data-sql-server.md)  
[Referência de método de tipo de dados hierarchyid]()
  
