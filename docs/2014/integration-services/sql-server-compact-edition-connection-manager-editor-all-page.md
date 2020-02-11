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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055464"
---
# <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>Editor do Gerenciador de Conexões do SQL Server Compact Edition (Página Tudo)
  Use a caixa de diálogo **Gerenciador de Conexões do SQL Server Compact Edition** para especificar as propriedades de conexão com um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 Para saber mais sobre o Gerenciador de conexões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact Edition, consulte [Gerenciador de conexões do SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md).  
  
## <a name="options"></a>Opções  
 **Limite de redução automática**  
 Especifique a quantidade de espaço livre, em percentual, que será permitido no banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact antes que o processo de redução automática seja executado.  
  
 **Escalonamento de bloqueio padrão**  
 Especifique o número de bloqueios de banco de dados que o banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact adquire antes de tentar escalonar bloqueios.  
  
 **Tempo limite de bloqueio padrão**  
 Especifique o intervalo padrão, em milissegundos, que uma transação esperará por um bloqueio.  
  
 **Intervalo de liberação**  
 Especifique o intervalo, em segundos, entre transações confirmadas para liberar os dados para o disco.  
  
 **Identificador de localidade**  
 Especifique a LCID (Identificação de Localidade) no banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Tamanho máximo do buffer**  
 Especifique a quantidade máxima de memória, em quilobytes, que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact usa antes de liberar os dados para o disco.  
  
 **Tamanho máximo do banco de dados**  
 Especifique o tamanho máximo, em megabytes, do banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Mode**  
 Especifique o modo de arquivo no qual abrir o banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact. O valor padrão dessa propriedade é **Leitura Gravação**.  
  
 A opção Modo tem quatro valores, como descrito na tabela seguinte.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|**Somente leitura**|Especifica acesso somente de leitura ao banco de dados.|  
|**Leitura Gravação**|Especifica a permissão de leitura e gravação ao banco de dados.|  
|**Exclusivo**|Especifica o acesso exclusivo ao banco de dados.|  
|**Leitura compartilhada**|Especifica que outros usuários podem ler de banco de dados ao mesmo tempo.|  
  
 **Informações de persistência de segurança**  
 Especifique se as informações de segurança são retornadas como parte da cadeia de conexão. O valor padrão dessa opção é **False**.  
  
 **Diretório de arquivos temporários**  
 Especifique o local do arquivo de banco de dados temporário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Fonte de Dados**  
 Especifique o nome do banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
 **Senha**  
 Digite a senha para o banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Compact.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [&#40;página de conexão do editor do Gerenciador de conexões do SQL Server Compact Edition&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
  
