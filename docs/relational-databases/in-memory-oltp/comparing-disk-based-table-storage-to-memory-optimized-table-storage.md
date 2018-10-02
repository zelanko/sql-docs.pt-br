---
title: Comparando o armazenamento da tabela baseada em disco com o armazenamento da tabela com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: eacf443c-001a-445f-ad1c-5f5a45eca6f4
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 361abc38238916a6c2f98e088d8609e325237b33
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632914"
---
# <a name="comparing-disk-based-table-storage-to-memory-optimized-table-storage"></a>Comparando o armazenamento da tabela baseada em disco com o armazenamento da tabela com otimização de memória
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  
  
|Categorias|Tabela com base em disco|Tabela durável com otimização de memória|  
|----------------|-----------------------|-------------------------------------|  
|DDL|As informações de metadados são armazenadas em tabelas do sistema no grupo de arquivos primário do banco de dados e podem sem acessadas por meio de exibições de catálogo.|As informações de metadados são armazenadas em tabelas do sistema no grupo de arquivos primário do banco de dados e podem sem acessadas por meio de exibições de catálogo.|  
|Estrutura|As linhas são armazenadas em 8 mil páginas. Uma página armazena apenas linhas da mesma tabela.|As linhas são armazenadas como linhas individuais. Não há nenhuma estrutura de página. Duas linhas consecutivas em um arquivo de dados podem pertencer a diferentes tabelas com otimização de memória.|  
|Índices|Os índices são armazenados em uma estrutura de página semelhante às linhas de dados.|Somente a definição do índice é mantida (e não as linhas do índice). Os índices são mantidos na memória e regenerados quando a tabela com otimização de memória é carregada na memória como parte da reinicialização de um banco de dados. Uma vez que as linhas do índice não são mantidas, nenhum registro em log é feito para alterações de índice.|  
|Operação DML|A primeira etapa é localizar a página e então carregá-la no pool de buffers.<br /><br /> Insert<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] insere a linha na página responsável pela ordenação da linha no caso de índice clusterizado.<br /><br /> DELETE<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localiza a linha a ser excluída na página e marca-a como excluída.<br /><br /> Update<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localiza a linha na página. A atualização é feita in-loco para colunas que não são de chave. A atualização da coluna de chave é feita por uma operação de exclusão e inserção.<br /><br /> Depois que a operação DML é concluída, as páginas afetadas são liberadas no disco como parte da política do pool de buffers, do ponto de verificação ou da confirmação de transação para operações minimamente registradas em log. As operações de leitura/gravação em páginas geram E/S desnecessária.|Para tabelas com otimização de memória, contanto que os dados residam na memória, as operações DML são feitas diretamente na memória. Há um thread em segundo plano que lê os registros de log de tabelas com otimização de memória e os mantém nos arquivos delta e de dados. Uma atualização gera uma nova versão de linha. Mas uma atualização é registrada como uma exclusão seguida de uma inserção.|  
|Fragmentação de dados|A manipulação de dados fragmenta os dados, o que gera páginas parcialmente preenchidas e páginas logicamente consecutivas que não são contíguas no disco. Isso degrada o desempenho de acesso a dados e exige a desfragmentação de dados.|Os dados com otimização de memória não são armazenados em páginas, de modo que não há fragmentação de dados. No entanto, como as linhas são atualizadas e excluídas, os arquivos delta e de dados precisam ser compactados. Isso é feito por um thread MERGE em segundo plano com base em uma política de mesclagem.|  
  
## <a name="see-also"></a>Consulte Também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
