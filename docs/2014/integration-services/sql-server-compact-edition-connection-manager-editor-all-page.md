---
title: Editor do Gerenciador de Conexão de edição (página tudo) do SQL Server Compact | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact Connection Manager Editor
ms.assetid: f9fbff4b-c502-44b3-8e7b-398d66e82206
caps.latest.revision: 25
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1d74007858a1834b4d0aba5538e62824f7cee8c6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192106"
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
  
|Valor|Description|  
|-----------|-----------------|  
|**Somente Leitura**|Especifica acesso somente de leitura ao banco de dados.|  
|**Leitura Gravação**|Especifica a permissão de leitura e gravação ao banco de dados.|  
|**Exclusive**|Especifica o acesso exclusivo ao banco de dados.|  
|**Shared Read**|Especifica que outros usuários podem ler de banco de dados ao mesmo tempo.|  
  
 **Informações de Persistência de Segurança**  
 Especifique se as informações de segurança são retornadas como parte da cadeia de conexão. O valor padrão dessa opção é **False**.  
  
 **Diretório de Arquivo Temporário**  
 Especifique o local do arquivo de banco de dados temporário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Fonte de dados**  
 Especifique o nome do banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Senha**  
 Digite a senha para o banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor do Gerenciador de Conexão de edição do SQL Server Compact &#40;página de Conexão&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
  
