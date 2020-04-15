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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288736"
---
# <a name="desktop-database-drivers-architecture"></a>Arquitetura de drivers de banco de dados de área de trabalho
Esses drivers são projetados para uso no Microsoft Windows 95 ou posterior, ou no Windows NT 4.0 e no Windows 2000. Apenas aplicativos de 32 bits são suportados no Windows 95 ou posteriores; Aplicativos de 16 bits e 32 bits são suportados no Windows NT 4.0 e no Windows 2000.  
  
> [!NOTE]  
>  Para obter informações sobre a versão do ODBC a ser usada com esses drivers, consulte a *Referência do Programador ODBC*e as notas de versão passadas e atuais. Com exceção das áreas anotadas, esses drivers estão em conformidade com a *Referência do Programador ODBC.*  
  
 Os drivers de banco de dados de desktop da ODBC incluem drivers de 32 bits para Microsoft Access, dBASE, Microsoft Excel, Paradox e Text. Não estão incluídos drivers de 16 bits. (Um driver para Microsoft FoxPro está disponível separadamente.)  
  
 A arquitetura de aplicativo/driver no Windows 95 ou posterior é:  
  
 ![Arquitetura de driver de&#47;de aplicativos: Windows 95 e posterior](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 O uso desses drivers por aplicativos de 16 bits no Windows 95 não é suportado.  
  
 A arquitetura de aplicativos/driverno Windows NT 4.0 e Windows 2000 é:  
  
 ![Arquitetura do driver de&#47;de aplicativos: NT 4.0 e Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 Os drivers do banco de dados da área de trabalho são drivers de dois níveis. Em uma configuração de dois níveis, o driver não executa o processo de análise, validação, otimização e execução da consulta. Em vez disso, o Microsoft Jet executa essas tarefas. Processa chamadas de API ODBC e atua como um motor SQL. O Microsoft Jet tornou-se uma parte integral e inseparável dos drivers: É enviado com os motoristas e reside com os motoristas, mesmo que nenhum outro aplicativo no computador o use.  
  
 Os Drivers de banco de dados da área de trabalho consistem em seis drivers diferentes - ou, mais precisamente, um arquivo de driver (Odbcjt32.dll) que o ODBC [Driver Manager](../../odbc/reference/the-driver-manager.md) usa de seis maneiras diferentes. A bandeira DRIVERID na entrada de registro de uma fonte de dados determina qual driver no Odbcjt32.dll o Driver Manager usa. Um aplicativo passa esse sinalizador na seqüência de conexão incluída em uma chamada para **SQLDriverConnect**. Por padrão, o sinalizador é o ID do driver Microsoft Access.  
  
 O arquivo de configuração do driver altera o sinalizador DRIVERID na hora da configuração. Todos os drivers, exceto o driver Microsoft Access, possuem uma DLL de configuração associada. Quando você **clica** em Configurar no [Microsoft ODBC Data Source Administrator](../../odbc/admin/odbc-data-source-administrator.md) para uma fonte de dados, o instalador ODBC DLL (Odbcinst.dll) carrega a Configuração DLL. A configuração DLL exporta a função de instalador **ODBC SQLConfigDataSource**. Se uma alça de janela for passada para **SQLConfigDataSource,** esta função exibirá uma janela de configuração e altera o sinalizador DRIVERID de acordo com o driver selecionado na interface do usuário.  
  
 Quando um arquivo é criado de forma programática, uma alça de janela NULL é passada para **SQLConfigDataSource**, e a função cria uma fonte de dados dinamicamente, alterando o sinalizador DRIVERID de acordo com o argumento *lpszDriver* na chamada de função.  
  
 Odbcjt32.dll implementa funções ODBC em cima da API do Microsoft Jet. No entanto, não há mapeamento direto entre as funções ODBC e Microsoft Jet. Muitos fatores, como os modelos de cursor e mapeamento SQL, impedem uma correlação direta das funções.  
  
 O driver ODBC reside entre o motor Microsoft Jet e o ODBC Driver Manager. Algumas funções ODBC chamadas por um aplicativo são tratadas pelo Driver Manager e não passadas ao driver. Para essas funções, o Microsoft Jet nunca vê a chamada de função porque não tem uma conexão direta com o Driver Manager.
