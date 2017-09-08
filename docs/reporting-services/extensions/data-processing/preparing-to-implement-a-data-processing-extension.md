---
title: "Preparando para implementar uma extensão de processamento de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- interfaces [Reporting Services]
- data processing extensions [Reporting Services], implementing
ms.assetid: 698817e4-33da-4eb5-9407-4103e1c35247
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 6d516201d8018b1d58b77be8e3cf543745da037a
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="preparing-to-implement-a-data-processing-extension"></a>Preparando para implementar uma extensão de processamento de dados
  Antes de implementar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensão de processamento de dados, você deve definir as interfaces para implementar. Talvez você queira fornecer implementações específicas da extensão de todo o conjunto de interfaces, ou pode simplesmente deseja se concentrar sua implementação em um subconjunto, como o <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> e <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> interfaces na qual os clientes seriam interagir principalmente com um conjunto de resultados como um **DataReader** de objeto e usaria o [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] extensão de processamento de dados como uma ponte entre o conjunto de resultados e a fonte de dados.  
  
 Você pode implementar extensões de processamento de dados em um de dois modos:  
  
-   Suas classes de extensão de processamento de dados podem implementar o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] interfaces de provedor de dados e, opcionalmente, as interfaces de extensão de processamento de dados estendidas fornecidas pelo [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
-   As suas classes de extensão de processamento de dados podem implementar as interfaces de extensão de processamento de dados fornecidas pelo [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e, opcionalmente, as interfaces de extensão de processamento de dados estendidas.  
  
 Se a sua extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] não dará suporte a uma propriedade específica ou a um método, implemente a propriedade ou o método como sem-operação. Se um cliente esperar um comportamento específico, lance uma **NotSupportedException** exceção.  
  
> [!NOTE]  
>  Uma implementação sem-operação de uma propriedade ou método só se aplica às propriedades e aos métodos das interfaces que você optar por implementar. As interfaces opcionais que você preferir não implementar devem ser omitidas de seu assembly de extensão de processamento de dados. Para obter mais informações para saber se uma interface é obrigatória ou opcional, consulte a tabela mais adiante nesta seção.  
  
## <a name="required-extension-functionality"></a>Funcionalidade de extensão obrigatória  
 Cada extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] deve fornecer a seguinte funcionalidade:  
  
-   Abrir uma conexão para uma fonte de dados.  
  
-   Analisar uma consulta e retornar uma lista de nomes de campo para o conjunto de resultados.  
  
-   Executar uma consulta em relação à fonte de dados e retornar um conjunto de linhas.  
  
-   Passar parâmetros de valor único à consulta.  
  
-   Iterar por linhas do conjunto de linhas e recuperar dados.  
  
 Cada extensão de processamento de dados pode ser estendida para incluir a seguinte funcionalidade:  
  
-   Analisar uma consulta e retornar uma lista dos nomes de parâmetros usados na consulta.  
  
-   Analisar uma consulta e retornar a lista de campos pelos quais a consulta é agrupada.  
  
-   Analisar uma consulta e retornar a lista de campos pelos quais a consulta é classificada.  
  
-   Fornecer um nome de usuário e uma senha para conectar à fonte de dados que é independente da cadeia de conexão.  
  
-   Iterar por linhas do conjunto de linhas e recuperar metadados auxiliares sobre os valores de dados.  
  
-   Agregar dados no servidor.  
  
## <a name="available-extension-interfaces"></a>Interfaces de extensão disponíveis  
 A tabela a seguir descreve as interfaces disponíveis e se implementação é obrigatória ou opcional.  
  
|Interface|Description|Implementação|  
|---------------|-----------------|--------------------|  
|IDbConnection|Representa uma sessão exclusiva com uma fonte de dados. No caso de um sistema de banco de dados cliente/servidor, a sessão pode ser equivalente a uma conexão de rede com o servidor.|Obrigatório|  
|IDbConnectionExtension|Representa propriedades de conexão adicionais que podem ser implementadas através de extensões de processamento de dados do [!INCLUDE[ssRS](../../../includes/ssrs-md.md)] relativas a segurança e a autenticação.|Opcional|  
|IDbTransaction|Representa uma transação local.|Obrigatório|  
|IDbTransactionExtension|Representa propriedades de transação adicionais que podem ser implementadas através de extensões de processamento de dados do [!INCLUDE[ssRS](../../../includes/ssrs-md.md)].|Opcional|  
|IDbCommand|Representa uma consulta ou um comando usado durante a conexão a uma fonte de dados.|Obrigatório|  
|IDbCommandAnalysis|Representa informações de comando adicionais para a análise de uma consulta e para o retorno de uma lista de nomes de parâmetro usados na consulta.|Opcional|  
|IDataParameter|Representa um parâmetro ou par de nome/valor passado a um comando ou a uma consulta.|Obrigatório|  
|IDataParameterCollection|Representa uma coleção de todos os parâmetros relevantes a um comando ou a uma consulta.|Obrigatório|  
|IDataReader|Fornece um método de leitura de um fluxo de dados somente encaminhamento, somente leitura a partir da sua fonte de dados.|Obrigatório|  
|IDataReaderExtension|Fornece um método de leitura de um ou mais fluxos somente encaminhamento de conjuntos de resultados, obtidos pela execução de um comando em uma fonte de dados. Essa interface oferece suporte adicional para agregações de campo.|Opcional|  
|IExtension|Fornece a classe base para uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Também permite que um implementador inclua um nome localizado para a extensão e passe configurações do arquivo de configuração para a extensão.|Obrigatório|  
  
 As interfaces de extensão de processamento de dados são idênticas a um subconjunto das interfaces de provedor de dados, métodos e propriedades do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] sempre que possível. Para obter mais informações sobre a implementação de um provedor de dados completo do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], consulte "Implementando um provedor de dados .NET Framework" na sua documentação do SDK (Software Development Kit) do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
