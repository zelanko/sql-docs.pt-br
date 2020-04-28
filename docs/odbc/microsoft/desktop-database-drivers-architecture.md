---
title: Arquitetura de drivers de banco de dados de desktop | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae6fb72bb3ed0a9bca1571eb572bbfbd20fe9995
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288736"
---
# <a name="desktop-database-drivers-architecture"></a>Arquitetura de drivers de banco de dados de área de trabalho
Esses drivers são projetados para uso no Microsoft Windows 95 ou posterior, ou no Windows NT 4,0 e no Windows 2000. Somente aplicativos de 32 bits têm suporte no Windows 95 ou posterior; Há suporte para aplicativos de 16 bits e de 32 bits no Windows NT 4,0 e no Windows 2000.  
  
> [!NOTE]  
>  Para obter informações sobre a versão do ODBC a ser usada com esses drivers, consulte a *referência do programador de ODBC*e notas de versão anteriores e atuais. Exceto pelas áreas indicadas, esses drivers estão em conformidade com a *referência do programador de ODBC*.  
  
 Os drivers de banco de dados da área de trabalho ODBC incluem drivers de 32 bits para Microsoft Access, dBASE, Microsoft Excel, Paradox e Text. Nenhum driver de 16 bits está incluído. (Um driver para o Microsoft FoxPro está disponível separadamente.)  
  
 A arquitetura de aplicativo/driver no Windows 95 ou posterior é:  
  
 ![Arquitetura de driver de&#47;de aplicativo: Windows 95 e posterior](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 Não há suporte para o uso desses drivers em aplicativos de 16 bits no Windows 95.  
  
 A arquitetura do aplicativo/driver no Windows NT 4,0 e no Windows 2000 é:  
  
 ![Arquitetura de driver de&#47;de aplicativo: NT 4,0 e Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 Os drivers de banco de dados da área de trabalho são drivers de duas camadas. Em uma configuração de duas camadas, o driver não executa o processo de análise, validação, otimização e execução da consulta. Em vez disso, o Microsoft Jet executa essas tarefas. Ele processa chamadas da API do ODBC e atua como um mecanismo do SQL. O Microsoft Jet tornou-se um integral, inseparáveis parte dos drivers: ele é fornecido com os drivers e reside com os drivers, mesmo que nenhum outro aplicativo no computador o use.  
  
 Os drivers de banco de dados da área de trabalho consistem em seis drivers diferentes – ou, mais precisamente, um arquivo de driver (Odbcjt32. dll) que o [Gerenciador de driver](../../odbc/reference/the-driver-manager.md) ODBC usa de seis maneiras diferentes. O sinalizador de DRIVERid na entrada de registro para uma fonte de dados determina qual driver em Odbcjt32. dll o Gerenciador de driver usa. Um aplicativo passa esse sinalizador na cadeia de conexão incluída em uma chamada para **SQLDriverConnect**. Por padrão, o sinalizador é a ID do driver do Microsoft Access.  
  
 O arquivo de instalação do driver altera o sinalizador do DRIVERid no momento da instalação. Todos os drivers, exceto o driver do Microsoft Access, têm uma DLL de instalação associada. Quando você clica em **instalação** no [administrador de fonte de dados ODBC da Microsoft](../../odbc/admin/odbc-data-source-administrator.md) para uma fonte de dados, a DLL do ODBC Installer (Odbcinst. DLL) carrega a DLL de instalação. A DLL de instalação exporta a função **SQLConfigDataSource**do ODBC Installer. Se um identificador de janela for passado para **SQLConfigDataSource**, essa função exibirá uma janela de instalação e alterará o sinalizador de DriverID de acordo com o driver selecionado na interface do usuário.  
  
 Quando um arquivo é criado programaticamente, um identificador de janela nulo é passado para **SQLConfigDataSource**e a função cria uma fonte de dados dinamicamente, alterando o sinalizador de DriverID de acordo com o argumento *lpszDriver* na chamada de função.  
  
 Odbcjt32. dll implementa funções ODBC sobre a API do Microsoft Jet. No entanto, não há mapeamento direto entre as funções ODBC e Microsoft Jet. Muitos fatores, como os modelos de cursor e o mapeamento de SQL, impedem uma correlação direta das funções.  
  
 O driver ODBC reside entre o mecanismo do Microsoft Jet e o Gerenciador de driver ODBC. Algumas funções ODBC chamadas por um aplicativo são manipuladas pelo Gerenciador de driver e não são passadas para o driver. Para essas funções, o Microsoft Jet nunca vê a chamada de função porque não tem uma conexão direta com o Gerenciador de driver.
