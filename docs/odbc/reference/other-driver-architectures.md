---
title: Outras Arquiteturas de Driver | Microsoft Docs
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
ms.openlocfilehash: ae047fe8014b806d3bda8b0513521b4ddda072a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280526"
---
# <a name="other-driver-architectures"></a>Outras arquiteturas do driver
Alguns drivers ODBC não estão estritamente de acordo com a arquitetura descrita anteriormente. Isso pode ser porque os motoristas executam funções diferentes das de um motorista oDBC tradicional, ou não são motoristas no sentido normal.  
  
## <a name="driver-as-a-middle-component"></a>Driver como um componente médio  
 O driver ODBC pode residir entre o Driver Manager e um ou mais outros drivers ODBC. Quando o driver no meio é capaz de trabalhar com várias fontes de dados, ele age como um despachante de chamadas ODBC (ou chamadas traduzidas apropriadamente) para outros módulos que realmente acessam as fontes de dados. Nesta arquitetura, o motorista no meio está assumindo parte do papel de motorista.  
  
 Outro exemplo desse tipo de driver é um programa espião para ODBC, que intercepta e copia funções ODBC sendo enviadas entre o Driver Manager e o driver. Esta camada pode ser usada para imitar um driver ou um aplicativo. Para o Gerenciador de driver, a camada parece ser o driver; para o driver, a camada parece ser o Driver Manager.  
  
## <a name="heterogeneous-join-engines"></a>Motores de adesão heterogêneos  
 Alguns drivers ODBC são construídos sobre um mecanismo de consulta para realizar adesões heterogêneas. Em uma arquitetura de um mecanismo de adesão heterogêneo (veja a ilustração a seguir), o motorista aparece no aplicativo como um driver, mas aparece em outra instância do Driver Manager como um aplicativo. Este driver processa uma adesão heterogênea do aplicativo, chamando declarações SQL separadas em drivers para cada banco de dados aderido.  
  
 ![Arquitetura de um mecanismo de junção heterogêneo](../../odbc/reference/media/fig3-4.gif "fig3-4")  
  
 Essa arquitetura fornece uma interface comum para o aplicativo acessar dados de diferentes bancos de dados. Ele pode usar uma maneira comum de recuperar metadados, como informações sobre colunas especiais (identificadores de linha), e pode chamar funções comuns de catálogo para recuperar informações do dicionário de dados. Ao chamar a função **ODBC de SQLStatistics,** por exemplo, o aplicativo pode recuperar informações sobre os índices nas tabelas a serem aderidas, mesmo que as tabelas estejam em dois bancos de dados separados. O processador de consulta não precisa se preocupar sobre como os bancos de dados armazenam metadados.  
  
 O aplicativo também tem acesso padrão aos tipos de dados. O ODBC define tipos comuns de dados SQL para os quais os tipos de dados específicos do DBMS são mapeados. Um aplicativo pode ligar para **o SQLGetTypeInfo** para recuperar informações sobre tipos de dados em diferentes bancos de dados.  
  
 Quando o aplicativo gera uma instrução de adesão heterogênea, o processador de consulta nesta arquitetura analisa a instrução SQL e, em seguida, gera instruções SQL separadas para cada banco de dados a ser juntado. Usando metadados sobre cada driver, o processador de consulta pode determinar a adesão mais eficiente e inteligente. Por exemplo, se a declaração se juntar a duas tabelas em um banco de dados com uma tabela em outro banco de dados, o processador de consulta pode juntar as duas tabelas em um banco de dados antes de juntar o resultado com a tabela do outro banco de dados.  
  
## <a name="odbc-on-the-server"></a>ODBC no Servidor  
 Os drivers ODBC podem ser instalados em um servidor para que possam ser usados por aplicativos em qualquer uma série de máquinas clientes. Nesta arquitetura (veja a ilustração a seguir), um driver manager e um único driver ODBC são instalados em cada cliente, e outro Driver Manager e uma série de drivers ODBC são instalados no servidor. Isso permite que cada cliente acesse uma variedade de drivers usados e mantidos no servidor.  
  
 ![Arquitetura dos drivers ODBC em um servidor](../../odbc/reference/media/fig3-5.gif "FIG3-5")  
  
 Uma vantagem dessa arquitetura é a manutenção e configuração eficientes do software. Os drivers só precisam ser atualizados em um lugar: no servidor. Usando fontes de dados do sistema, as fontes de dados podem ser definidas no servidor para uso de todos os clientes. As fontes de dados não precisam ser definidas no cliente. O pool de conexões pode ser usado para agilizar o processo pelo qual os clientes se conectam a fontes de dados.  
  
 O driver no cliente geralmente é um motorista muito pequeno que transfere a chamada do Driver Manager para o servidor. Sua pegada pode ser significativamente menor do que os drivers ODBC totalmente funcionais no servidor. Nesta arquitetura, os recursos do cliente podem ser liberados se o servidor tiver mais poder de computação. Além disso, a eficiência e a segurança de todo o sistema podem ser aprimoradas instalando servidores de backup e realizando balanceamento de carga para otimizar o uso do servidor.
