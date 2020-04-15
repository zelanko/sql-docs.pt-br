---
title: SQLConfigDataSource (driver de acesso) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48668525b578845fc330881d7c7de503d69d0928
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284046"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (Driver do Access)
> [!NOTE]  
>  Este tópico fornece informações específicas do Access Driver. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 A função **SQLConfigDataSource,** usada para adicionar, modificar ou excluir uma fonte de dados, usa dinamicamente as seguintes palavras-chave.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|SEQÜÊNCIA DE COLISÃO|A seqüência em que os campos são classificados.<br /><br /> Isso define a mesma opção **que A seqüência de colisão** na caixa de diálogo de configuração.|  
|COMPACT_DB|Realiza a compactação de dados em um arquivo de banco de dados. Tem o seguinte formato: COMPACT_DB= \<<path_name><optionaL_sort_order>> opcional DE ENCRYPT.<br /><br /> Ao usar a palavra-chave COMPACT_DB na mesma declaração com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, compactar um banco de dados e especificar um DSN é um processo de duas etapas.|  
|CREATE_DB|Cria um arquivo de banco de dados. Tem o seguinte formato: CREATE_DB=<path_name>>><\<de optional_sort ordem optional_ENCRYPT palavra-chave>, onde o nome do caminho é o caminho completo para um banco de dados microsoft access. Um erro será retornado se o nome do caminho especificar um banco de dados existente. A ordem de classificação será configurada na caixa de diálogo Novo banco de dados exibida quando o botão Criar for pressionado na caixa de diálogo Configuração do Microsoft Access. Se nenhuma ordem de classificação for especificada, o General será usado.<br /><br /> Ao usar a palavra-chave CREATE_DB na mesma declaração com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, criar um banco de dados e especificar um DSN é um processo de duas etapas. Ao usar a palavra-chave CREATE_DB, se o nome de caminho do banco de dados Microsoft Access a ser criado contiver um ou mais espaços, então o nome de caminho inteiro deve ser incluído por aspas duplas, como mostrado nos exemplos a seguir:<br /><br /> "C:\ARQUIVOS DO PROGRAMA\ARQUIVOS COMUNS\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb (sem aspas necessárias)|  
|CREATE_SYSDB|Cria um arquivo de banco de dados do sistema. Tem o seguinte formato:\<CREATE_SYSDB= \<nome de caminho>> de ordem de classificação opcional, onde o nome do caminho é o caminho completo para um banco de dados microsoft access. Um erro será retornado se o nome do caminho especificar um banco de dados existente. A ordem de classificação será configurada na caixa de diálogo **Novo banco** de dados exibida quando o botão **Criar** for clicado na caixa de diálogo **ODBC Microsoft Access Setup.** Se nenhuma ordem de classificação for especificada, o General será usado.|  
|CREATE_V2DB|Cria um arquivo de banco de dados compatível com o Microsoft Access 2.0. Tem o seguinte formato:\<CREATE_V2DB= \<nome de caminho>> de ordem de classificação opcional, onde o nome do caminho é o caminho completo para um banco de dados microsoft access. Um erro será retornado se o nome do caminho especificar um banco de dados existente. A ordem de classificação será configurada na caixa de diálogo Novo banco de dados exibida quando o botão Criar for pressionado na caixa de diálogo Configuração do Microsoft Access. Se nenhuma ordem de classificação for especificada, o General será usado.<br /><br /> Ao usar a palavra-chave CREATE_V2DB na mesma declaração com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, criar um banco de dados e especificar um DSN é um processo de duas etapas.<br /><br /> Ao usar a palavra-chave CREATE_V2DB, se o nome de caminho do banco de dados Microsoft Access a ser criado contiver um ou mais espaços, então o nome de caminho inteiro deve ser incluído por aspas duplas, como mostrado nos exemplos a seguir:<br /><br /> "C:\ARQUIVOS DO PROGRAMA\ARQUIVOS COMUNS\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb (sem aspas necessárias)|  
|Dbq|O nome do arquivo do banco de dados.<br /><br /> Isso define a mesma opção que o **Banco de Dados** na caixa de diálogo de configuração.|  
|Defaultdir|A especificação do caminho para o arquivo do banco de dados.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção **que Description** na caixa de diálogo de configuração.|  
|DRIVER|A especificação do caminho para o driver DLL.|  
|DRIVERID|Uma id inteira para o motorista.  25 (Acesso Microsoft)|  
|Fil|Tipo de arquivo MS Acesso para Acesso Microsoft|  
|IMPLICITCOMMITSYNC|Determina se o driver do Microsoft Access executará compromissos internos ou implícitos de forma assíncrona. Esse valor é inicialmente definido como "Sim", o que significa que o driver do Microsoft Access aguardará os compromissos em uma transação interna/implícita a ser concluída.<br /><br /> O valor desta opção não deve ser alterado sem uma consideração cuidadosa das consequências. Para obter mais informações sobre a opção, consulte o *Guia do Programador do Motor do Banco de Dados microsoft jet*.<br /><br /> Isso define a mesma opção **que ImplicitCommitSync** na caixa de diálogo de configuração.|  
|Maxbuffersize|O tamanho do buffer interno, em kilobytes, que é usado pelo Microsoft Access para transferir dados de e para o disco. O tamanho padrão do buffer é de 2048 KB (exibido como 2048). Qualquer valor inteiro divisível por 256 pode ser usado. Isso define a mesma opção **que o Tamanho do buffer** na caixa de diálogo de configuração.|  
|MAXSCANROWS|O número de linhas a serem digitalizadas ao definir o tipo de dados de uma coluna com base nos dados existentes.<br /><br /> Um número de 1 a 16 pode ser inserido para as linhas para escanear. O valor é padrão para 8; se for definido como 0, todas as linhas são digitalizadas. (Um número fora do limite retornará um erro.)<br /><br /> Isso define a mesma opção **que Linhas para Scan na** caixa de diálogo de configuração.|  
|PAGETIMEOUT|Especifica o período de tempo, em milissegundos, que uma página (se não usada) permanece no buffer antes de ser removida. O padrão é de cinco décimos de segundo (0,5 segundos). Observe que essa opção se aplica a todas as fontes de dados que usam o driver ODBC.<br /><br /> Isso define a mesma opção que **o Tempo de página** na caixa de diálogo de configuração.|  
|PWD|A senha.|  
|READONLY|TRUE para tornar somente leitura de arquivo; FALSO para fazer o arquivo não ler somente.<br /><br /> Isso define a mesma opção **que Read Only** na caixa de diálogo de configuração.|  
|REPAIR_DB|Repara um banco de dados danificado por uma falha que ocorre durante o processo de confirmação.<br /><br /> Ao usar a palavra-chave REPAIR_DB na mesma declaração com uma palavra-chave DSN, este driver ignora a palavra-chave DSN. Portanto, reparar um banco de dados e especificar um DSN é um processo de duas etapas.|  
|SYSTEMDB|Para o driver Microsoft Access, a especificação do caminho para o arquivo do banco de dados do sistema.<br /><br /> Isso define a mesma opção que o **Banco de Dados** do Sistema na caixa de diálogo de configuração.|  
|Tópicos|O número de roscas de fundo para o motor usar. Este valor é padrão para 3, mas pode ser alterado.<br /><br /> Isso define a mesma opção **que os Threads** na caixa de diálogo de configuração.|  
|UID|Para o driver Microsoft Access, o nome de id do usuário usado para login.|  
|USERCOMMITSYNC|Determina se o driver do Microsoft Access executará transações definidas pelo usuário de forma assíncrona. Esse valor é inicialmente definido como "Sim", o que significa que o driver do Microsoft Access aguardará os compromissos em uma transação definida pelo usuário para ser concluída.<br /><br /> O valor desta opção não deve ser alterado sem uma consideração cuidadosa das consequências. Para obter mais informações sobre a opção, consulte o *Guia do Programador do Motor do Banco de Dados microsoft jet*.<br /><br /> Isso define a mesma opção **que UserCommitSync** na caixa de diálogo de configuração.|
