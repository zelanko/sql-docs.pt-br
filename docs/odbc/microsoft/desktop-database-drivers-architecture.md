---
title: Arquitetura de Drivers de banco de dados de área de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 975e70038bc78962691ea30f885dd0050e508753
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="desktop-database-drivers-architecture"></a>Arquitetura de Drivers de banco de dados de área de trabalho
Esses drivers são projetados para uso no Microsoft Windows 95 ou posterior, ou Windows NT 4.0 e Windows 2000. Aplicativos de 32 bits só têm suporte no Windows 95 ou posterior; aplicativos de 16 bits e 32 bits têm suporte no Windows NT 4.0 e Windows 2000.  
  
> [!NOTE]  
>  Para obter informações sobre a versão do ODBC a ser usado com esses drivers, consulte o *referência do programador de ODBC*e notas de versão atuais e anteriores. Exceto para áreas observadas, estes drivers estão em conformidade com a *referência do programador de ODBC*.  
  
 Os Drivers de banco de dados de área de trabalho do ODBC incluem drivers de 32 bits para Microsoft Access, dBASE, Microsoft Excel, Paradox e texto. Não drivers de 16 bits são incluídos. (Um driver para Microsoft FoxPro está disponível separadamente.)  
  
 A arquitetura do aplicativo/driver no Windows 95 ou posterior é:  
  
 ![Aplicativo&#47;a arquitetura do driver: Windows 95 e posterior](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 Não há suporte para o uso desses drivers por aplicativos de 16 bits no Windows 95.  
  
 A arquitetura do aplicativo/driver no Windows NT 4.0 e Windows 2000 é:  
  
 ![Aplicativo&#47;a arquitetura do driver: NT 4.0 e Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 Os Drivers de banco de dados de área de trabalho são drivers de duas camadas. Em uma configuração de duas camadas, o driver não executa o processo de análise, validação, otimização e executar a consulta. Em vez disso, o Microsoft Jet executa essas tarefas. Ele processa as chamadas da API do ODBC e atua como um mecanismo SQL. Microsoft Jet tornou-se uma parte integrante e inseparável drivers: ele é fornecido com os drivers e reside com os drivers, mesmo se nenhum outro aplicativo no computador utiliza.  
  
 Os Drivers de banco de dados de área de trabalho consistem em seis diferentes drivers — ou, mais precisamente, o driver de um arquivo (Odbcjt32.dll) que o ODBC [Gerenciador de Driver](../../odbc/reference/the-driver-manager.md) usa seis maneiras diferentes. O sinalizador DRIVERID na entrada do registro para uma fonte de dados determina qual driver em Odbcjt32.dll usa o Gerenciador de Driver. Um aplicativo passa esse sinalizador na cadeia de conexão incluída em uma chamada para **SQLDriverConnect**. Por padrão, o sinalizador é a ID do driver do Microsoft Access.  
  
 O arquivo de instalação do driver altera o sinalizador DRIVERID no momento da instalação. Todos os drivers, exceto o driver do Microsoft Access tem uma DLL de configuração associada. Quando você clica em **instalação** no [administrador de fonte de dados do Microsoft ODBC](../../odbc/admin/odbc-data-source-administrator.md) para uma fonte de dados, o instalador do ODBC DLL (Odbcinst) carrega a DLL de configuração. A instalação do DLL exporta a função do instalador ODBC **SQLConfigDataSource**. Se um identificador de janela é passado para **SQLConfigDataSource**, essa função exibe uma janela de instalação e altera o sinalizador DRIVERID de acordo com o driver selecionado na interface do usuário.  
  
 Quando um arquivo é criado por meio de programação, um identificador de janela nulo é passado para **SQLConfigDataSource**, e a função cria uma fonte de dados dinamicamente, alterar o sinalizador DRIVERID de acordo com o *lpszDriver*argumento na chamada de função.  
  
 Odbcjt32.dll implementa funções ODBC sobre a API do Microsoft Jet. No entanto, há nenhum mapeamento direto entre funções de ODBC e Microsoft Jet. Muitos fatores, como os modelos de cursor e o mapeamento de SQL, impedir que uma correlação direta das funções.  
  
 O driver ODBC reside entre o Microsoft Jet e o Gerenciador de Driver ODBC. Algumas funções ODBC chamadas por um aplicativo são tratadas pelo Gerenciador de Driver e não são passadas para o driver. Essas funções, o Microsoft Jet nunca vê a função chamada porque ela não tem uma conexão direta para o Gerenciador de Driver.
