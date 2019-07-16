---
title: Outras arquiteturas do Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], heterogeneous join engines
- drivers [ODBC], ODBC on the server
- ODBC architecture [ODBC], drivers
- heterogeneous join engines[ODBC]
- drivers [ODBC], middle component
ms.assetid: 1cad06ee-5940-4361-8d01-7d850db1dd66
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8dbfb09a261d7499e07137b7ed830d5a5b92dc73
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086010"
---
# <a name="other-driver-architectures"></a>Outras arquiteturas do driver
Alguns drivers ODBC não estritamente em conformidade com a arquitetura descrita anteriormente. Isso pode ocorrer porque os drivers de realizar tarefas diferentes daqueles de um driver ODBC tradicional ou não são drivers no sentido de normal.  
  
## <a name="driver-as-a-middle-component"></a>Driver como um componente central  
 O driver ODBC pode residir entre o Gerenciador de Driver e um ou mais outros drivers ODBC. Quando o driver no meio é capaz de trabalhar com várias fontes de dados, ele atua como um distribuidor de chamadas ODBC (ou chamadas adequadamente traduzidas) para outros módulos que realmente os acessam as fontes de dados. Nessa arquitetura, o driver no meio está levando alguns da função de um Gerenciador de Driver.  
  
 Outro exemplo desse tipo de driver é um programa spy para ODBC, que intercepta e copia funções ODBC que estão sendo enviadas entre o Gerenciador de Driver e o driver. Essa camada pode ser usada para emular um driver ou um aplicativo. Para o Gerenciador de Driver, a camada parece ser o driver; para o driver, a camada parece ser o Gerenciador de Driver.  
  
## <a name="heterogeneous-join-engines"></a>Mecanismos de junção heterogêneo  
 Alguns drivers ODBC baseiam-se um mecanismo de consulta para executar junções heterogêneas. Em uma arquitetura de um mecanismo de junção heterogêneo (consulte a ilustração a seguir), o driver é exibido para o aplicativo como um driver, mas aparece como outra instância do Gerenciador de Driver como um aplicativo. Esse driver processa uma junção heterogênea do aplicativo chamando instruções separadas do SQL nos drivers para cada banco de dados Unido.  
  
 ![Arquitetura de um mecanismo de junção heterogêneo](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 Essa arquitetura fornece uma interface comum para o aplicativo acessar dados de bancos de dados diferentes. Ele pode usar uma maneira comum para recuperar metadados, tais como informações sobre colunas especiais (identificadores de linha), e ele pode chamar funções comuns de catálogo para recuperar informações do dicionário de dados. Chamando a função ODBC **SQLStatistics**, por exemplo, o aplicativo pode recuperar informações sobre os índices nas tabelas a serem agrupados, mesmo se as tabelas estiverem em dois bancos de dados separados. O processador de consulta não precisa se preocupar sobre como os bancos de dados armazenam metadados.  
  
 O aplicativo também tem acesso padrão para tipos de dados. ODBC define tipos de dados SQL comuns mapeados para tipos de dados específicos de DBMS. Um aplicativo pode chamar **SQLGetTypeInfo** para recuperar informações sobre tipos de dados de bancos de dados diferentes.  
  
 Quando o aplicativo gera uma instrução de junção heterogêneo, o processador de consultas nesta arquitetura analisa a instrução SQL e, em seguida, gera instruções SQL separadas para cada banco de dados a ser unida. Usando metadados sobre cada driver, o processador de consultas pode determinar a junção inteligente e mais eficiente. Por exemplo, se a instrução une duas tabelas em um banco de dados com uma tabela em outro banco de dados, o processador de consulta pode unir as duas tabelas em um banco de dados antes de se juntar o resultado com a tabela a partir de outro banco de dados.  
  
## <a name="odbc-on-the-server"></a>ODBC no servidor  
 Drivers ODBC podem ser instalados em um servidor para que eles podem ser usados por aplicativos em qualquer um de uma série de computadores cliente. Nessa arquitetura (consulte a ilustração a seguir), um Gerenciador de Driver e um único driver ODBC são instalados em cada cliente e outro gerenciador de Driver e uma série de drivers ODBC estão instalados no servidor. Isso permite que cada acesso de cliente para uma variedade de drivers usados e mantidos no servidor.  
  
 ![Arquitetura dos drivers ODBC em um servidor](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 Uma vantagem dessa arquitetura é a configuração e manutenção de software eficiente. Drivers só precisam ser atualizados em um único lugar: no servidor. Usando fontes de dados do sistema, fontes de dados podem ser definidas no servidor para uso por todos os clientes. As fontes de dados não precisam ser definidas no cliente. Pooling de Conexão pode ser usado para simplificar o processo pelo qual os clientes se conectam a fontes de dados.  
  
 O driver no cliente geralmente é um driver muito pequeno que transfere a chamada de Gerenciador de Driver ao servidor. Seu impacto pode ser significativamente menor do que os drivers ODBC totalmente funcionais no servidor. Nessa arquitetura, os recursos de cliente podem ser liberados se o servidor tiver mais potência de computação. Além disso, a eficiência e a segurança de todo o sistema podem ser aprimorados ao instalar servidores de backup e realizar o balanceamento de carga para otimizar o uso do servidor.
