---
title: Replicar tabelas e índices particionados | Microsoft Docs
ms.custom: ''
ms.date: 09/10/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- partitioned indexes [SQL Server], replicating
- partitioned tables [SQL Server], replicating
- replication [SQL Server], partitioned tables
- publishing [SQL Server replication], partitioned tables
- transactional replication, partitioned tables
ms.assetid: c9fa81b1-6c81-4c11-927b-fab16301a8f5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f2201be33df4346ab2afa812828ab9655b0ed2be
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793290"
---
# <a name="replicate-partitioned-tables-and-indexes"></a>Replicar tabelas e índices particionados
  O particionamento facilita o gerenciamento de grandes tabelas ou índices, permitindo o acesso e o gerenciamento de subconjuntos de dados de forma rápida e eficaz, ao mesmo tempo em que mantém a integridade geral da coleção de dados. Para obter mais informações, consulte [Partitioned Tables and Indexes](../../partitions/partitioned-tables-and-indexes.md). A replicação dá suporte ao particionamento fornecendo um conjunto de propriedades que especificam como tabelas e índices particionados devem ser tratados.  
  
## <a name="article-properties-for-transactional-and-merge-replication"></a>Propriedades de artigo para replicação transacional e de mesclagem  
 A tabela a seguir lista os objetos que são usados para particionar dados.  
  
|Object|Criado com|  
|------------|----------------------|  
|Tabela ou índice particionado|CREATE TABLE ou CREATE INDEX|  
|Função Partition|CREATE PARTITION FUNCTION|  
|Esquema de partição|CREATE PARTITION SCHEME|  
  
 O primeiro conjunto de propriedades relacionadas ao particionamento são as opções de esquema de artigo que determinam se os objetos de particionamento devem ser copiados para o Assinante. Essas opções de esquema podem ser definidas das seguintes formas:  
  
-   Na página **Propriedades do Artigo** do Assistente para Nova Publicação ou na caixa de Propriedades de Publicação. Para copiar os objetos listados na tabela anterior, especifique um valor de `true` para as propriedades **copiar esquemas de particionamento de tabela** e **copiar esquemas de particionamento de índice**. Para obter informações sobre como acessar a página **Propriedades do artigo**, consulte [Exibir e modificar as propriedades da publicação](view-and-modify-publication-properties.md).  
  
-   Usando o parâmetro *schema_option* de um dos procedimentos armazenados a seguir:  
  
    -   [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) ou [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) para replicação transacional  
  
    -   [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) ou [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) para replicação de mesclagem  
  
     Para copiar os objetos listados na tabela anterior, especifique os valores de opção de esquema apropriados. Para obter informações sobre como especificar opções de esquema, consulte [Specify Schema Options](specify-schema-options.md).  
  
 A replicação copia objetos para o Assinante durante a sincronização inicial. Se o esquema de partição usar grupos de arquivo diferentes do grupo de arquivo PRIMARY, esses grupos deverão existir no Assinante antes da sincronização inicial.  
  
 Depois que o Assinante é inicializado, as alterações de dados são propagadas para o Assinante e aplicadas nas partições apropriadas. Porém, as alterações no esquema de partição não são suportadas. Replicação transacional e de mesclagem não dão suporte a replicação dos seguintes comandos: ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME ou a instrução REBUILD WITH PARTITION de ALTER INDEX.  As alterações associadas a eles não serão replicadas automaticamente para o Assinante. É responsabilidade do usuário fazer alterações semelhantes manualmente no Assinante.  
  
## <a name="replication-support-for-partition-switching"></a>Suporte de replicação para alternância de partição  
 Um dos principais benefícios do particionamento de tabela é a possibilidade de mover subconjuntos de dados entre partições com rapidez e eficiência. Os dados são movidos com o comando SWITCH PARTITION. Por padrão, quando uma tabela é habilitada para replicação, as operações SWITCH PARTITION são bloqueadas pelos seguintes motivos:  
  
-   Se os dados forem movidos para ou de uma tabela que existe no Publicador, mas não existe no Assinante, ambos ficarão inconsistentes entre si. Esse problema ocorre normalmente quando os dados são movidos para ou de uma tabela de preparação.  
  
-   Se o Assinante tiver uma definição diferente para a tabela particionada da definição do Publicador, o Agente de Distribuição falhará ao tentar aplicar as alterações no Assinante.  
  
 Apesar destes possíveis problemas, a alternância de partição pode ser habilitada para replicação transacional. Antes de habilitá-la, verifique se todas as tabelas que estão envolvidas na alternância de partição existem no Publicador e no Assinante e verifique se as definições de tabela e de partição são iguais.  
  
 Quando as partições têm o esquema de partição exato nos publicadores e assinantes, você pode ativar o *allow_partition_switch* junto com *replication_partition_switch* , que somente replicará a instrução switch da partição para o assinante. Você também pode ativar o *allow_partition_switch* sem replicar o DDL. Isto é útil no caso em que você deseja reverter meses antigos da partição, mas persistir a partição replicada no local durante outro ano para fins de backup no assinante.  
  
 Se você habilitar a alternância de partição no SQL Server 2008 R2 até a versão atual, talvez também seja necessário realizar operações de divisão e mesclagem em um futuro próximo. Antes de executar uma operação de divisão ou mesclagem em uma tabela replicada, certifique-se de que a partição em questão não tenha nenhum comando replicado pendente. Você também deve garantir que nenhuma operação DML seja executada na partição durante as operações de divisão e mesclagem. Se houver transações não processadas pelo leitor de log, ou se as operações DML forem executadas em uma partição de uma tabela replicada enquanto uma operação de divisão ou mesclagem é executada (envolvendo a mesma partição), isso pode levar a um erro de processamento com o agente de leitor de log. Para corrigir o erro, talvez isso exija uma reinicialização da assinatura.  
  
> [!WARNING]  
>  Você não deveria habilitar o switch de partição para publicações ponto a ponto, devido à coluna oculta que é usada para detectar e resolver conflitos.  
  
### <a name="enabling-partition-switching"></a>Habilitando a alternância de partição  
 As propriedades a seguir para publicações transacionais permitem que os usuários controlem o comportamento da alternância de partição em um ambiente replicado:  
  
-   **\@allow_partition_switch**, quando definido como `true`, SWITCH PARTITION pode ser executado no banco de dados de publicação.  
  
-   **\@replicate_partition_switch** determina se a instrução SWITCH PARTITION DDL deve ser replicada para assinantes. Essa opção é válido somente quando  **\@allow_partition_switch** é definido como `true`.  
  
 Você pode definir essas propriedades usando [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql) quando a publicação é criada ou usando [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) depois da criação da publicação. Como observado anteriormente, a replicação de mesclagem não dá suporte à alternância de partição. Para executar SWITCH PARTITION em uma tabela que é habilitada para replicação de mesclagem, remova a tabela da publicação.  
  
## <a name="see-also"></a>Consulte também  
 [Publicar dados e objetos de banco de dados](publish-data-and-database-objects.md)  
  
  
