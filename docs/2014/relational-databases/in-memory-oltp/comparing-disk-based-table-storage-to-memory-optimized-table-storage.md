---
title: Comparando o armazenamento da tabela baseada em disco com o armazenamento da tabela com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: eacf443c-001a-445f-ad1c-5f5a45eca6f4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: be224cdd8c3221f1e7796e15c9c0132aeb99bcd7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62990668"
---
# <a name="comparing-disk-based-table-storage-to-memory-optimized-table-storage"></a>Comparando o armazenamento da tabela baseada em disco com o armazenamento da tabela com otimização de memória
  
  
|Categories|Tabela com base em disco|Tabela durável com otimização de memória|  
|----------------|-----------------------|-------------------------------------|  
|DDL|As informações de metadados são armazenadas em tabelas do sistema no grupo de arquivos primário do banco de dados e podem sem acessadas por meio de exibições de catálogo.|As informações de metadados são armazenadas em tabelas do sistema no grupo de arquivos primário do banco de dados e podem sem acessadas por meio de exibições de catálogo.|  
|Estrutura|As linhas são armazenadas em 8 mil páginas. Uma página armazena apenas linhas da mesma tabela.|As linhas são armazenadas como linhas individuais. Não há nenhuma estrutura de página. Duas linhas consecutivas em um arquivo de dados podem pertencer a diferentes tabelas com otimização de memória.|  
|Índices|Os índices são armazenados em uma estrutura de página semelhante às linhas de dados.|Somente a definição do índice é mantida (e não as linhas do índice). Os índices são mantidos na memória e regenerados quando a tabela com otimização de memória é carregada na memória como parte da reinicialização de um banco de dados. Uma vez que as linhas do índice não são mantidas, nenhum registro em log é feito para alterações de índice.|  
|Operação DML|A primeira etapa é localizar a página e então carregá-la no pool de buffers.<br /><br /> Insert<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] insere a linha na página responsável pela ordenação da linha no caso de índice clusterizado.<br /><br /> DELETE<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localiza a linha a ser excluída na página e marca-a como excluída.<br /><br /> Update<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localiza a linha na página. A atualização é feita in-loco para colunas que não são de chave. A atualização da coluna de chave é feita por uma operação de exclusão e inserção.<br /><br /> Depois que a operação DML é concluída, as páginas afetadas são liberadas no disco como parte da política do pool de buffers, do ponto de verificação ou da confirmação de transação para operações minimamente registradas em log. As operações de leitura/gravação em páginas geram E/S desnecessária.|Para tabelas com otimização de memória, contanto que os dados residam na memória, as operações DML são feitas diretamente na memória. Há um thread em segundo plano que lê os registros de log de tabelas com otimização de memória e os mantém nos arquivos delta e de dados. Uma atualização gera uma nova versão de linha. Mas uma atualização é registrada como uma exclusão seguida de uma inserção.|  
|Fragmentação de dados|A manipulação de dados fragmenta os dados, o que gera páginas parcialmente preenchidas e páginas logicamente consecutivas que não são contíguas no disco. Isso degrada o desempenho de acesso a dados e exige a desfragmentação de dados.|Os dados com otimização de memória não são armazenados em páginas, de modo que não há fragmentação de dados. No entanto, como as linhas são atualizadas e excluídas, os arquivos delta e de dados precisam ser compactados. Isso é feito por um thread MERGE em segundo plano com base em uma política de mesclagem.|  
  
## <a name="see-also"></a>Consulte também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
