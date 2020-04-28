---
title: Definindo opções programaticamente para o driver de acesso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], setting options programmatically
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
ms.assetid: 1690eb71-0cd3-4c00-9e15-f6a3ac5316dd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a90f0a20569a2a0a5bb93dec7aa4b95b50093dc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300786"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Configurar opções programaticamente para drivers do Access

|Opção|Descrição|Método|  
|------------|-----------------|------------|  
|Tamanho do Buffer|O tamanho do buffer interno, em kilobytes, que é usado pelo Microsoft Access para transferir dados de e para o disco. O tamanho de buffer padrão é 2048 KB (exibido como 2048). Qualquer valor inteiro divisível por 256 pode ser inserido.|Para definir essa opção dinamicamente, use a palavra-chave MAXBUFFERSIZE em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como folha de pagamento ou equipe.|Para definir essa opção dinamicamente, use a palavra-chave **DSN** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Banco de dados|Uma fonte de dados do Microsoft Access pode ser configurada sem selecionar ou criar um banco de dado. Se nenhum banco de dados for fornecido na instalação, será solicitado que o usuário escolha um arquivo de banco de dados ao conectar-se à fonte.|Para definir essa opção dinamicamente, use a palavra-chave **DBQ** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Descrição|Uma descrição opcional dos dados na fonte de dados; por exemplo, "data de contratação, histórico de salários e revisão atual de todos os funcionários".|Para definir essa opção dinamicamente, use a palavra-chave **Description** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Exclusivo|Se a caixa **exclusiva** for selecionada, o banco de dados será aberto em modo exclusivo e poderá ser acessado por apenas um usuário por vez. O desempenho é aprimorado quando executado em modo exclusivo.|Para definir essa opção dinamicamente, use a palavra-chave **Exclusive** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|ImplicitCommitSync|Determina como as alterações feitas fora de uma transação são gravadas no banco de dados. Esse valor é inicialmente definido como "Sim", o que significa que o driver do Microsoft Access aguardará a conclusão de confirmações em uma transação interna/implícita.|Essa opção está incluída na caixa de diálogo **definir opções avançadas** para o driver do Microsoft Access.|  
|Tempo limite da página|Especifica o período de tempo, em milissegundos, que uma página (se não usada) permanece no buffer antes de ser removida. Para o driver do Microsoft Access, o padrão é 500 milissegundos (0,5 segundos). Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> O tempo limite da página não pode ser 0 devido a um atraso inerente. O tempo limite da página não pode ser menor que o atraso inerente, mesmo que a opção de tempo limite da página esteja definida abaixo desse valor.|Para definir essa opção dinamicamente, use a palavra-chave **PAGETIMEOUT** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Somente leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use a palavra-chave **ReadOnly** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Banco de dados do sistema|O caminho completo do banco de dados do sistema do Microsoft Access a ser usado com o banco de dados do Microsoft Access que você deseja acessar.<br /><br /> Clique no botão **banco de dados do sistema** para selecionar o banco de dados do sistema a ser usado. O driver ODBC Microsoft Access solicita ao usuário um nome e uma senha. O nome padrão é admin e a senha padrão no Microsoft Access para o usuário administrador é uma cadeia de caracteres vazia.<br /><br /> Para aumentar a segurança do seu banco de dados do Microsoft Access, crie um novo usuário para substituir o usuário administrador e excluir o usuário administrador ou altere os objetos aos quais o usuário administrador tem acesso.|Para definir essa opção dinamicamente, use a palavra-chave **SYSTEMDB** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Threads|O número de threads em segundo plano a ser usado pelo mecanismo. Para o driver do Microsoft Access, esse valor usa como padrão 3, mas pode ser alterado. O usuário pode desejar aumentar o número de threads se houver uma grande quantidade de atividade no banco de dados.<br /><br /> Essa opção está incluída na caixa de diálogo **definir opções avançadas** para o driver do Microsoft Access.|Para definir essa opção dinamicamente, use a palavra-chave **threads** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|UserCommitSync|Determina se o driver do Microsoft Access executará uma transação explícita definida pelo usuário de forma assíncrona. Esse valor é inicialmente definido como "Sim", o que significa que o driver do Microsoft Access aguardará a conclusão de confirmações em uma transação definida pelo usuário.<br /><br /> Definir essa opção como false pode ter consequências imprevisíveis em um ambiente de vários usuários.|Para definir essa opção dinamicamente, use a palavra-chave **USERCOMMITSYNC** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|
