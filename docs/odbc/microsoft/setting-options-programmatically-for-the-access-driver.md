---
title: Definindo opções programáticas para o driver de acesso | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300786"
---
# <a name="setting-options-programmatically-for-the-access-driver"></a>Configurar opções programaticamente para drivers do Access

|Opção|Descrição|Método|  
|------------|-----------------|------------|  
|Tamanho do Buffer|O tamanho do buffer interno, em kilobytes, que é usado pelo Microsoft Access para transferir dados de e para o disco. O tamanho padrão do buffer é de 2048 KB (exibido como 2048). Qualquer valor inteiro divisível por 256 pode ser inserido.|Para definir essa opção dinamicamente, use a palavra-chave MAXBUFFERSIZE em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Nome da Fonte de Dados|Um nome que identifica a fonte de dados, como Folha de Pagamento ou Pessoal.|Para definir essa opção dinamicamente, use a palavra-chave **DSN** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Banco de dados|Uma fonte de dados do Microsoft Access pode ser configurada sem selecionar ou criar um banco de dados. Se nenhum banco de dados for fornecido após a configuração, o usuário será solicitado a escolher um arquivo de banco de dados ao se conectar à fonte de dados.|Para definir essa opção dinamicamente, use a palavra-chave **DBQ** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Descrição|Uma descrição opcional dos dados na fonte de dados; por exemplo, "Data de contratação, histórico salarial e revisão atual de todos os funcionários."|Para definir essa opção dinamicamente, use a palavra-chave **DESCRIPTION** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Exclusivo|Se a caixa **Exclusiva** for selecionada, o banco de dados será aberto no modo Exclusivo e poderá ser acessado por apenas um usuário por vez. O desempenho é aprimorado ao ser executado no modo Exclusivo.|Para definir essa opção dinamicamente, use a palavra-chave **EXCLUSIVE** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|ImplicitCommitSync|Determina como as alterações feitas fora de uma transação são escritas no banco de dados. Esse valor é inicialmente definido como "Sim", o que significa que o driver do Microsoft Access aguardará os compromissos em uma transação interna/implícita a ser concluída.|Esta opção está incluída na caixa de diálogo **Definir opções avançadas** para o driver Microsoft Access.|  
|Tempo de página|Especifica o período de tempo, em milissegundos, que uma página (se não usada) permanece no buffer antes de ser removida. Para o driver Microsoft Access, o padrão é de 500 milissegundos (0,5 segundos). Essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> O tempo de saída da página não pode ser 0 por causa de um atraso inerente. O tempo limite da página não pode ser menor do que o atraso inerente, mesmo que a opção de tempo limite da página esteja definida abaixo desse valor.|Para definir essa opção dinamicamente, use a palavra-chave **PAGETIMEOUT** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Somente leitura|Designa o banco de dados como somente leitura.|Para definir essa opção dinamicamente, use a palavra-chave **READONLY** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Banco de dados do sistema|O caminho completo do banco de dados do sistema Microsoft Access a ser usado com o banco de dados microsoft access que você deseja acessar.<br /><br /> Clique no botão **Banco de dados** do sistema para selecionar o banco de dados do sistema a ser usado. O driver ODBC Microsoft Access solicita ao usuário um nome e senha. O nome padrão é Admin e a senha padrão no Microsoft Access para o usuário do Admin é uma seqüência vazia.<br /><br /> Para aumentar a segurança do seu banco de dados microsoft access, crie um novo usuário para substituir o usuário do Administrador e excluir o usuário do Administrador ou alterar os objetos aos quais o usuário do Administrador tem acesso.|Para definir essa opção dinamicamente, use a palavra-chave **SYSTEMDB** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|Threads|O número de roscas de fundo para o motor usar. Para o driver Microsoft Access, esse valor é padrão para 3, mas pode ser alterado. O usuário pode querer aumentar o número de threads se houver uma grande quantidade de atividade no banco de dados.<br /><br /> Esta opção está incluída na caixa de diálogo **Definir opções avançadas** para o driver Microsoft Access.|Para definir essa opção dinamicamente, use a palavra-chave **THREADS** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|  
|UserCommitSync|Determina se o driver do Microsoft Access executará uma transação explícita definida pelo usuário de forma assíncrona. Esse valor é inicialmente definido como "Sim", o que significa que o driver do Microsoft Access aguardará os compromissos em uma transação definida pelo usuário para ser concluída.<br /><br /> Definir essa opção como False pode ter consequências imprevisíveis em um ambiente de vários usuários.|Para definir essa opção dinamicamente, use a palavra-chave **USERCOMMITSYNC** em uma chamada para [SQLConfigDataSource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md).|
