---
title: Arquivos e grupos de Arquivos de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3d75dee637a5579ca3f189e14333fbf9356623d0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62917273"
---
# <a name="database-files-and-filegroups"></a>Arquivos e grupos de arquivos do banco de dados
  Todo o banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem, no mínimo, dois arquivos de sistema operacional: um arquivo de dados e um arquivo de log. Os arquivos de dados contêm dados e objetos como tabelas, índices, procedimentos armazenados e exibições. Os arquivos de log contêm as informações necessárias para recuperar todas as transações no banco de dados. Os arquivos de dados podem ser agrupados em grupos de arquivos para propósitos de alocação e administração.  
  
## <a name="database-files"></a>Arquivos do banco de dados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possuem três tipos de arquivos, como mostrado na tabela a seguir.  
  
|Arquivo|DESCRIÇÃO|  
|----------|-----------------|  
|Primária|O arquivo de dados primário contém as informações de inicialização do banco de dados e aponta para os outros arquivos no banco de dados. Dados do usuário e objetos podem ser armazenados neste arquivo ou em arquivos de dados secundários. Todo banco de dados possui um arquivo de dados primário. A extensão de nome de arquivo indicada para arquivos de dados primários é .mdf.|  
|Secundário|Os arquivos de dados secundários são opcionais, definidos pelo usuário, e armazenam dados do usuário. Arquivos secundários podem ser usados para distribuir os dados entre os diversos discos, colocando cada arquivo em uma unidade de disco diferente. Além disso, caso um banco de dados exceda o tamanho máximo em um único arquivo Windows, será possível usar arquivos de dados secundários, assim, o banco de dados continuará a crescer.<br /><br /> A extensão de nome de arquivo indicada para arquivos de dados secundários é .ndf.|  
|Log de Transações|Os arquivos de log de transações armazenam as informações de log usadas para recuperar o banco de dados. Deve haver, no mínimo, um arquivo de log para cada banco de dados. A extensão de nome de arquivo indicada para arquivos de transação é .ldf.|  
  
 Por exemplo, pode-se criar um simples banco de dados nomeado como **Vendas** que tenha um arquivo primário com todos os dados e objetos, e um arquivo de log que tenha as informações de log de transação. Como alternativa, pode-se criar um banco de dados mais complexo nomeado como **Pedidos** que tenha um arquivo primário e cinco arquivos secundários. Os dados e objetos no banco de dados distribuem-se pelos seis arquivos, e os quatro arquivos de log contêm as informações do log de transação.  
  
 Por padrão, os dados e logs de transação são colocados na mesma unidade e caminho. Isto é feito para controlar os sistemas de um único disco. Porém, isto não é o ideal para ambientes de produção. Recomendamos que você coloque os dados e arquivos de log em discos separados.  
  
## <a name="filegroups"></a>Grupos de arquivos  
 Todo banco de dados possui um grupo de arquivo primário. Este grupo de arquivo contém o arquivo de dados primário e qualquer um dos arquivos secundários que não foram colocados em outros grupos de arquivos. Grupos de arquivos definidos pelo usuário podem ser criados para agrupar os arquivos de dados para fins administrativos, de alocação de dados e de posicionamento.  
  
 Por exemplo, três arquivos, Data1.ndf, Data2.ndf, e Data3.ndf, podem ser criados em três unidades de disco, respectivamente, e atribuídos ao grupo de arquivos **fgroup1**. Uma tabela pode ser criada especificamente no grupo de arquivos **fgroup1**. As consultas para obter dados da tabela serão distribuídas pelos três discos; isso melhorará o desempenho. A mesma melhora no desenvolvimento pode acontecer, usando um único arquivo criado em um conjunto distribuído RAID (redundant array of independent disks). Porém, arquivos e grupos de arquivos permitem que novos arquivos sejam facilmente adicionados aos novos discos.  
  
 Todos os arquivos de dados são armazenados nos grupos de arquivos listados na tabela a seguir.  
  
|Grupo de arquivos|Descrição|  
|---------------|-----------------|  
|Primária|O grupo de arquivos que contém o arquivo primário. Todas as tabelas do sistema são alocadas no grupo de arquivos primário.|  
|Definido pelo usuário|Qualquer grupo de arquivos que seja criado especificamente pelo usuário quando o usuário cria primeiro ou modifica depois o banco de dados.|  
  
### <a name="default-filegroup"></a>Grupo de arquivos padrão  
 Quando objetos são criados no banco de dados sem especificar a qual grupo de arquivos eles pertencem, os objetos são atribuídos ao grupo de arquivos padrão. A qualquer hora, um grupo de arquivos é designado como o grupo de arquivos padrão. Os arquivos no grupo de arquivos padrão devem ser grandes o suficientes para armazenar qualquer objeto novo alocado a outros grupos de arquivo.  
  
 O grupo de arquivos PRIMÁRIO é o grupo de arquivos padrão, a menos que seja alterado usando a instrução ALTER DATABASE. A alocação para os objetos de sistema e de tabelas permanece no grupo de arquivos PRIMÁRIO, e não no novo grupo de arquivos padrão.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
 [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
 [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  
