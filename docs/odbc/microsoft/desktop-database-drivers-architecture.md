---
title: Arquitetura de Drivers de banco de dados da área de trabalho | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01de6a3707ea2ed96399c678625f3e94c13fc5db
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649564"
---
# <a name="desktop-database-drivers-architecture"></a>Arquitetura de drivers de banco de dados de área de trabalho
Esses drivers são projetados para uso no Microsoft Windows 95 ou posterior, ou Windows NT 4.0 e Windows 2000. Somente aplicativos de 32 bits têm suporte no Windows 95 ou posterior; aplicativos de 16 bits e 32 bits têm suporte no Windows NT 4.0 e Windows 2000.  
  
> [!NOTE]  
>  Para obter informações sobre a versão do ODBC a serem usados com esses drivers, consulte o *referência do programador de ODBC*e notas de versão passadas e atuais. Exceto para áreas indicadas, esses drivers estão em conformidade com o *referência do programador de ODBC*.  
  
 Os Drivers de banco de dados do ODBC da área de trabalho incluem os drivers de 32 bits para Microsoft Access, dBASE, Microsoft Excel, Paradox e texto. Não 16 - bit drivers estão incluídos. (Um driver para Microsoft FoxPro está disponível separadamente.)  
  
 A arquitetura do aplicativo/driver no Windows 95 ou posterior é:  
  
 ![Aplicativo&#47;arquitetura do driver: Windows 95 e posterior](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 Não há suporte para o uso desses drivers por aplicativos de 16 bits no Windows 95.  
  
 A arquitetura do aplicativo/driver no Windows NT 4.0 e Windows 2000 é:  
  
 ![Aplicativo&#47;arquitetura do driver: NT 4.0 e Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 Os Drivers de banco de dados de área de trabalho são drivers de duas camadas. Em uma configuração de duas camadas, o driver não executa o processo de análise, validação, otimizando e execução da consulta. Em vez disso, o Microsoft Jet executa essas tarefas. Ele processa as chamadas à API de ODBC e atua como um mecanismo SQL. Microsoft Jet se tornou uma parte integral e inseparável dos drivers: ele é fornecido com os drivers e reside com os drivers, mesmo se nenhum outro aplicativo no computador utiliza.  
  
 Os Drivers de banco de dados de área de trabalho consistem em seis drivers diferentes — ou, mais precisamente, o driver de um arquivo (Odbcjt32.dll) que o ODBC [Gerenciador de Driver](../../odbc/reference/the-driver-manager.md) usa seis maneiras diferentes. O sinalizador DRIVERID na entrada do registro para uma fonte de dados determina qual driver em Odbcjt32.dll o Gerenciador de Driver usa. Um aplicativo passa esse sinalizador na cadeia de conexão incluída em uma chamada para **SQLDriverConnect**. Por padrão, o sinalizador é a ID do driver do Microsoft Access.  
  
 O arquivo de instalação do driver altera o sinalizador DRIVERID no momento da instalação. Todos os drivers, exceto o driver do Microsoft Access tem uma DLL de instalação associado. Quando você clica em **instalação** na [administrador de fonte de dados do Microsoft ODBC](../../odbc/admin/odbc-data-source-administrator.md) para uma fonte de dados, o instalador ODBC DLL (Odbcinst) carrega a DLL de instalação. A instalação DLL exporta a função do instalador ODBC **SQLConfigDataSource**. Se um identificador de janela é passado para **SQLConfigDataSource**, esta função exibe uma janela de instalação e altera o sinalizador DRIVERID de acordo com o driver selecionado da interface do usuário.  
  
 Quando um arquivo é criado por meio de programação, um identificador de janela NULL é passado para **SQLConfigDataSource**, e a função cria uma fonte de dados dinamicamente, alterando o sinalizador DRIVERID de acordo com o *lpszDriver*argumento na chamada de função.  
  
 Odbcjt32.dll implementa funções ODBC sobre a API do Microsoft Jet. No entanto, há nenhum mapeamento direto entre as funções do Microsoft Jet e ODBC. Vários fatores, como os modelos de cursor e o mapeamento de SQL, impedir que uma correlação direta das funções.  
  
 O driver ODBC reside entre o mecanismo Microsoft Jet e o Gerenciador de Driver ODBC. Algumas funções ODBC chamadas por um aplicativo são tratadas pelo Gerenciador de Driver e não são passadas para o driver. Para essas funções, o Microsoft Jet nunca vê a função chamada porque ele não tem uma conexão direta para o Gerenciador de Driver.
