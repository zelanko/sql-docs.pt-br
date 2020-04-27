---
title: Editor do Gerenciador de conexões do SQL Server Compact Edition (página todas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact Connection Manager Editor
ms.assetid: f9fbff4b-c502-44b3-8e7b-398d66e82206
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8a26587f9dd426cdf53a3a53a36d0e81e95ebf77
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66055464"
---
# <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>Editor do Gerenciador de Conexões do SQL Server Compact Edition (Página Tudo)
  Use a caixa de diálogo **Gerenciador de Conexões do SQL Server Compact Edition** para especificar as propriedades de conexão com um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 Para saber mais sobre o Gerenciador de conexões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact Edition, consulte [Gerenciador de conexões do SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md).  
  
## <a name="options"></a>Opções  
 **Limite de AutoShrink**  
 Especifique a quantidade de espaço livre, em percentual, que será permitido no banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact antes que o processo de redução automática seja executado.  
  
 **Escalonamento de Bloqueio Padrão**  
 Especifique o número de bloqueios de banco de dados que o banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact adquire antes de tentar escalonar bloqueios.  
  
 **Tempos Limite de Bloqueio Padrão**  
 Especifique o intervalo padrão, em milissegundos, que uma transação esperará por um bloqueio.  
  
 **Intervalo de Liberação**  
 Especifique o intervalo, em segundos, entre transações confirmadas para liberar os dados para o disco.  
  
 **Identificador de Localidade**  
 Especifique a LCID (Identificação de Localidade) no banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Tamanho Máximo do Buffer**  
 Especifique a quantidade máxima de memória, em quilobytes, que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact usa antes de liberar os dados para o disco.  
  
 **Tamanho Máximo do Banco de Dados**  
 Especifique o tamanho máximo, em megabytes, do banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Modo**  
 Especifique o modo de arquivo no qual abrir o banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact. O valor padrão dessa propriedade é **Leitura Gravação**.  
  
 A opção Modo tem quatro valores, como descrito na tabela seguinte.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Somente Leitura**|Especifica acesso somente de leitura ao banco de dados.|  
|**Leitura Gravação**|Especifica a permissão de leitura e gravação ao banco de dados.|  
|**Exclusive**|Especifica o acesso exclusivo ao banco de dados.|  
|**Shared Read**|Especifica que outros usuários podem ler de banco de dados ao mesmo tempo.|  
  
 **Persist Security Info**  
 Especifique se as informações de segurança são retornadas como parte da cadeia de conexão. O valor padrão dessa opção é **False**.  
  
 **Diretório de Arquivo Temporário**  
 Especifique o local do arquivo de banco de dados temporário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Fonte de Dados**  
 Especifique o nome do banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Senha**  
 Digite a senha para o banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página de Conexão&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
  
