---
title: Configuração do mecanismo - Filestream do banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], about FILESTREAM
ms.assetid: 641a10a1-ae52-4d26-8f1c-a032a4aeff02
caps.latest.revision: 12
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 82bf651e6242be7e1835caac7fd7d3419b51cf31
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187693"
---
# <a name="database-engine-configuration---filestream"></a>Configuração do Mecanismo de Banco de Dados – Fluxo de arquivos
  Use esta página para habilitar FILESTREAM para esta instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. FILESTREAM integra o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com um NTFS no sistema de arquivos, armazenando `varbinary(max)` dados de objeto binário grande (BLOB) como arquivos no sistema de arquivos. [!INCLUDE[tsql](../../includes/tsql-md.md)] podem inserir, atualizar, consultar, pesquisar e fazer backup de dados FILESTREAM. As interfaces do sistema de arquivos do Win32 fornecem acesso de streaming aos dados.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Habilitar FILESTREAM para acesso Transact-SQL**  
 Selecione para habilitar FILESTREAM para acesso [!INCLUDE[tsql](../../includes/tsql-md.md)] . Este controle deve ser verificado antes que as demais opções de controle fiquem disponíveis.  
  
 **Habilitar FILESTREAM para acesso de fluxo de E/S de arquivo**  
 Selecione para habilitar o acesso de fluxo Win32 para FILESTREAM.  
  
 **Nome de compartilhamento do Windows**  
 Use este controle para digitar o nome do compartilhamento do Windows no qual os dados FILESTREAM serão armazenados.  
  
 **Permitir que clientes remotos tenham acesso de fluxo a dados FILESTREAM**  
 Selecione este controle para permitir que clientes remotos acessem dados FILESTREAM neste servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Habilitar e configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
