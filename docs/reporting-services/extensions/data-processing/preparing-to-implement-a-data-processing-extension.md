---
title: Preparando a implementação de uma extensão de processamento de dados | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- interfaces [Reporting Services]
- data processing extensions [Reporting Services], implementing
ms.assetid: 698817e4-33da-4eb5-9407-4103e1c35247
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b3ae11d41956f37f1a203235abad71639f942ae7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63193898"
---
# <a name="preparing-to-implement-a-data-processing-extension"></a>Preparando para implementar uma extensão de processamento de dados
  Antes de implementar a extensão de processamento de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], você deve definir as interfaces a serem implementadas. Talvez você deseje fornecer implementações específicas à extensão de todo o conjunto de interfaces ou simplesmente pode desejar concentrar a implementação em um subconjunto, como as interfaces <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> e <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand>, nas quais os clientes poderão interagir principalmente com um conjunto de resultados como um objeto **DataReader** e usarão a extensão de processamento de dados do [!INCLUDE[ssRS](../../../includes/ssrs.md)] como uma ponte entre o conjunto de resultados e a fonte de dados.  
  
 Você pode implementar extensões de processamento de dados em um de dois modos:  
  
-   As classes de extensão de processamento de dados podem implementar as interfaces de provedor de dados do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] e, opcionalmente, as interfaces de extensão de processamento de dados estendidas fornecidas pelo [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
-   As suas classes de extensão de processamento de dados podem implementar as interfaces de extensão de processamento de dados fornecidas pelo [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e, opcionalmente, as interfaces de extensão de processamento de dados estendidas.  
  
 Se a sua extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] não dará suporte a uma propriedade específica ou a um método, implemente a propriedade ou o método como sem-operação. Se um cliente esperar um comportamento específico, gere uma exceção **NotSupportedException**.  
  
> [!NOTE]  
>  Uma implementação sem-operação de uma propriedade ou método só se aplica às propriedades e aos métodos das interfaces que você optar por implementar. As interfaces opcionais que você preferir não implementar devem ser omitidas de seu assembly de extensão de processamento de dados. Para obter mais informações para saber se uma interface é obrigatória ou opcional, consulte a tabela mais adiante nesta seção.  
  
## <a name="required-extension-functionality"></a>Funcionalidade de extensão obrigatória  
 Cada extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] deve fornecer a seguinte funcionalidade:  
  
-   Abrir uma conexão para uma fonte de dados.  
  
-   Analisar uma consulta e retornar uma lista de nomes de campo para o conjunto de resultados.  
  
-   Executar uma consulta na fonte de dados e retornar um conjunto de linhas.  
  
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
  
|Interface|Descrição|Implementação|  
|---------------|-----------------|--------------------|  
|IDbConnection|Representa uma sessão exclusiva com uma fonte de dados. No caso de um sistema de banco de dados cliente/servidor, a sessão pode ser equivalente a uma conexão de rede com o servidor.|Obrigatório|  
|IDbConnectionExtension|Representa propriedades de conexão adicionais que podem ser implementadas através de extensões de processamento de dados do [!INCLUDE[ssRS](../../../includes/ssrs.md)] relativas a segurança e a autenticação.|Opcional|  
|IDbTransaction|Representa uma transação local.|Obrigatório|  
|IDbTransactionExtension|Representa propriedades de transação adicionais que podem ser implementadas através de extensões de processamento de dados do [!INCLUDE[ssRS](../../../includes/ssrs.md)].|Opcional|  
|IDbCommand|Representa uma consulta ou um comando usado durante a conexão a uma fonte de dados.|Obrigatório|  
|IDbCommandAnalysis|Representa informações de comando adicionais para a análise de uma consulta e para o retorno de uma lista de nomes de parâmetro usados na consulta.|Opcional|  
|IDataParameter|Representa um parâmetro ou par de nome/valor passado a um comando ou a uma consulta.|Obrigatório|  
|IDataParameterCollection|Representa uma coleção de todos os parâmetros relevantes a um comando ou a uma consulta.|Obrigatório|  
|IDataReader|Fornece um método de leitura de um fluxo de dados somente encaminhamento, somente leitura a partir da sua fonte de dados.|Obrigatório|  
|IDataReaderExtension|Fornece um método de leitura de um ou mais fluxos somente encaminhamento de conjuntos de resultados, obtidos pela execução de um comando em uma fonte de dados. Essa interface oferece suporte adicional para agregações de campo.|Opcional|  
|IExtension|Fornece a classe base para uma extensão de processamento de dados do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Também permite que um implementador inclua um nome localizado para a extensão e passe configurações do arquivo de configuração para a extensão.|Obrigatório|  
  
 As interfaces de extensão de processamento de dados são idênticas a um subconjunto das interfaces de provedor de dados, métodos e propriedades do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] sempre que possível. Para obter mais informações sobre a implementação de um provedor de dados completo do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], consulte "Implementando um provedor de dados .NET Framework" na sua documentação do SDK (Software Development Kit) do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementando uma extensão de processamento de dados](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensões do Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
