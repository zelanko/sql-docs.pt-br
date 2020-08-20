---
description: Outras arquiteturas do driver
title: Outras arquiteturas de driver | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44a09eb786abc9f43e25ea105e25e8fdefcdff86
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499659"
---
# <a name="other-driver-architectures"></a>Outras arquiteturas do driver
Alguns drivers ODBC não estão estritamente de acordo com a arquitetura descrita anteriormente. Isso pode ocorrer porque os drivers executam tarefas diferentes das de um driver ODBC tradicional ou não são drivers no sentido normal.  
  
## <a name="driver-as-a-middle-component"></a>Driver como um componente do meio  
 O driver ODBC pode residir entre o Gerenciador de driver e um ou mais drivers ODBC. Quando o driver no meio é capaz de trabalhar com várias fontes de dados, ele atua como um Dispatcher de chamadas ODBC (ou chamadas traduzidas adequadamente) para outros módulos que realmente acessam as fontes de dados. Nessa arquitetura, o driver no meio está assumindo uma parte da função de um Gerenciador de driver.  
  
 Outro exemplo desse tipo de driver é um programa Spy para ODBC, que intercepta e copia as funções ODBC que estão sendo enviadas entre o Gerenciador de driver e o driver. Essa camada pode ser usada para emular um driver ou um aplicativo. Para o Gerenciador de driver, a camada parece ser o driver; para o driver, a camada parece ser o Gerenciador de driver.  
  
## <a name="heterogeneous-join-engines"></a>Mecanismos de junção heterogêneas  
 Alguns drivers ODBC são criados com base em um mecanismo de consulta para executar junções heterogêneas. Em uma arquitetura de um mecanismo de junção heterogênea (consulte a ilustração a seguir), o driver aparecerá para o aplicativo como um driver, mas aparecerá para outra instância do Gerenciador de driver como um aplicativo. Esse driver processa uma junção heterogênea do aplicativo chamando instruções SQL separadas em drivers para cada banco de dados Unido.  
  
 ![Arquitetura de um mecanismo de junção heterogêneo](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 Essa arquitetura fornece uma interface comum para que o aplicativo acesse dados de diferentes bancos de dado. Ele pode usar uma maneira comum de recuperar metadados, como informações sobre colunas especiais (identificadores de linha), e pode chamar funções de catálogo comuns para recuperar informações de dicionário de dados. Ao chamar a função ODBC **SQLStatistics**, por exemplo, o aplicativo pode recuperar informações sobre os índices nas tabelas a serem Unidas, mesmo que as tabelas estejam em dois bancos de dados separados. O processador de consultas não precisa se preocupar em como os bancos de dados armazenam metadados.  
  
 O aplicativo também tem acesso padrão a tipos de dados. O ODBC define tipos de dados SQL comuns aos quais os tipos de dados específicos de DBMS são mapeados. Um aplicativo pode chamar **SQLGetTypeInfo** para recuperar informações sobre os tipos de dados em diferentes bancos.  
  
 Quando o aplicativo gera uma instrução de junção heterogênea, o processador de consultas nessa arquitetura analisa a instrução SQL e, em seguida, gera instruções SQL separadas para cada banco de dados a ser Unido. Usando metadados sobre cada Driver, o processador de consultas pode determinar a junção mais eficiente e inteligente. Por exemplo, se a instrução unir duas tabelas em um banco de dados com uma tabela em outro banco de dados, o processador de consultas poderá unir as duas tabelas em um banco de dados antes de ingressar o resultado com a tabela do outro banco de dados.  
  
## <a name="odbc-on-the-server"></a>ODBC no servidor  
 Os drivers ODBC podem ser instalados em um servidor para que possam ser usados por aplicativos em qualquer uma das séries de computadores cliente. Nessa arquitetura (consulte a ilustração a seguir), um Gerenciador de driver e um único driver ODBC são instalados em cada cliente, e outro gerenciador de driver e uma série de drivers ODBC são instalados no servidor. Isso permite que cada cliente acesse uma variedade de drivers usados e mantidos no servidor.  
  
 ![Arquitetura dos drivers ODBC em um servidor](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 Uma vantagem dessa arquitetura é a manutenção e a configuração de software eficientes. Os drivers só precisam ser atualizados em um único local: no servidor. Usando fontes de dados do sistema, as fontes de dados podem ser definidas no servidor para uso por todos os clientes. As fontes de dados não precisam ser definidas no cliente. O pooling de conexão pode ser usado para simplificar o processo pelo qual os clientes se conectam a fontes de dados.  
  
 O driver no cliente geralmente é um driver muito pequeno que transfere a chamada do Gerenciador de driver para o servidor. Sua superfície pode ser significativamente menor do que os drivers ODBC totalmente funcionais no servidor. Nessa arquitetura, os recursos do cliente poderão ser liberados se o servidor tiver mais capacidade computacional. Além disso, a eficiência e a segurança de todo o sistema podem ser aprimoradas instalando servidores de backup e executando o balanceamento de carga para otimizar o uso do servidor.
