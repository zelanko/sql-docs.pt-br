---
title: Comparar baseado em disco a armazenamento de tabela com otimização de memória
description: Aprenda a comparar o armazenamento de tabela com otimização de memória e baseado em disco nas categorias DDL, estrutura, índices, operação DML e fragmentação de dados.
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: eacf443c-001a-445f-ad1c-5f5a45eca6f4
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c747328877911d8f470b93f9937c1bc49466ddb3
ms.sourcegitcommit: d56a834269132a83e5fe0a05b033936776cda8bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91529451"
---
# <a name="comparing-disk-based-table-storage-to-memory-optimized-table-storage"></a>Comparando o armazenamento da tabela baseada em disco com o armazenamento da tabela com otimização de memória
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  
  
|Categorias|Tabela com base em disco|Tabela durável com otimização de memória|  
|----------------|-----------------------|-------------------------------------|  
|DDL|As informações de metadados são armazenadas em tabelas do sistema no grupo de arquivos primário do banco de dados e podem sem acessadas por meio de exibições de catálogo.|As informações de metadados são armazenadas em tabelas do sistema no grupo de arquivos primário do banco de dados e podem sem acessadas por meio de exibições de catálogo.|  
|Estrutura|As linhas são armazenadas em 8 mil páginas. Uma página armazena apenas linhas da mesma tabela.|As linhas são armazenadas como linhas individuais. Não há nenhuma estrutura de página. Duas linhas consecutivas em um arquivo de dados podem pertencer a diferentes tabelas com otimização de memória.|  
|Índices|Os índices são armazenados em uma estrutura de página semelhante às linhas de dados.|Somente a definição do índice é mantida (e não as linhas do índice). Os índices são mantidos na memória e regenerados quando a tabela com otimização de memória é carregada na memória como parte da reinicialização de um banco de dados. Uma vez que as linhas do índice não são mantidas, nenhum registro em log é feito para alterações de índice.|  
|Operação DML|A primeira etapa é localizar a página e então carregá-la no pool de buffers.<br /><br /> Inserir<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] insere a linha na página responsável pela ordenação da linha para índice clusterizado.<br /><br /> Excluir<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localiza a linha a ser excluída na página e marca-a como excluída.<br /><br /> Atualizar<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localiza a linha na página. A atualização é feita in-loco para colunas que não são de chave. A atualização da coluna de chave é feita por uma operação de exclusão e inserção.<br /><br /> Depois que a operação DML for concluída, as páginas afetadas serão liberadas no disco como parte da política do pool de buffers, do ponto de verificação ou da confirmação de transação para operações minimamente registradas. As operações de leitura/gravação em páginas geram E/S desnecessária.|Para tabelas com otimização de memória, contanto que os dados residam na memória, as operações DML são feitas diretamente na memória. Há um thread em segundo plano que lê os registros de log de tabelas com otimização de memória e os mantém nos arquivos delta e de dados. Uma atualização gera uma nova versão de linha. Mas uma atualização é registrada como uma exclusão seguida de uma inserção.|  
|Fragmentação de dados|A manipulação de dados fragmenta os dados, o que gera páginas parcialmente preenchidas e páginas logicamente consecutivas que não são contíguas no disco. Isso degrada o desempenho de acesso a dados e exige a desfragmentação de dados.|Os dados com otimização de memória não são armazenados em páginas, de modo que não há fragmentação de dados. No entanto, como as linhas são atualizadas e excluídas, os arquivos delta e de dados precisam ser compactados. Isso é feito por um thread MERGE em segundo plano com base em uma política de mesclagem.|  
  
## <a name="see-also"></a>Consulte Também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
