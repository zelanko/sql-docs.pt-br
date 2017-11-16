---
title: Tratamento de erros e avisos (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- errors [XML for Analysis]
- inline errors [XMLA]
- SOAP faults [XML for Analysis]
- XML for Analysis, errors
- faults [XML for Analysis]
- messages [XML for Analysis]
- XMLA, errors
- warnings [XML for Analysis]
- inline warnings [XMLA]
ms.assetid: ab895282-098d-468e-9460-032598961f45
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b1268714f696f852d999a833cf59e69be8c44bb3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="handling-errors-and-warnings-xmla"></a>Manipulando erros e avisos (XMLA)
  Tratamento de erros é necessário quando um XML for Analysis (XMLA) [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) ou [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) chamada de método não é executado, é executado com êxito, mas gera erros ou avisos, ou seja executado com êxito mas retorna resultados que contêm erros.  
  
|Erro|Relatório|  
|-----------|---------------|  
|A chamada de método XMLA não é executada|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna uma mensagem de falha SOAP que contém os detalhes da falha.<br /><br /> Para obter mais informações, consulte a seção [tratamento de falhas de SOAP](#handling_soap_faults).|  
|Erros ou avisos em uma chamada de método com êxito|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]inclui um [erro](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) ou [aviso](../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md) elemento para cada erro ou aviso, respectivamente, no [mensagens](../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md) propriedade o [raiz](../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md) elemento que contém os resultados da chamada de método.<br /><br /> Para obter mais informações, consulte a seção [Handling Errors and Warnings](#handling_errors_and_warnings).|  
|Erros no resultado de uma chamada de método com êxito|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]inclui um embutido **erro** ou **aviso** elemento para o erro ou aviso, respectivamente, no apropriada [célula](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md) ou [linha](../../analysis-services/xmla/xml-elements-properties/row-element-xmla.md) elemento dos resultados da chamada de método.<br /><br /> Para obter mais informações, consulte a seção [tratamento de erros e avisos embutidos](#handling_inline_errors_and_warnings).|  
  
##  <a name="handling_soap_faults"></a>Tratamento de falhas de SOAP  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna uma falha SOAP quando ocorrem as seguintes situações:  
  
-   A mensagem SOAP que contém o método XMLA não foi bem formada ou não pôde ser validada pela instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Houve um erro de comunicação ou outro erro envolvendo a mensagem SOAP que contém o método XMLA.  
  
-   O método XMLA não foi executado na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Os códigos de falha SOAP para XMLstartA começam com "XMLForAnalysis", seguido por um ponto e o código de resultado hexadecimal HRESULT. Por exemplo, um código de erro "`0x80000005`" é formatado como "`XMLForAnalysis.0x80000005`". Para obter mais informações sobre o formato de falha SOAP, consulte Falha Soap no protocolo SOAP 1.1 do W3C.  
  
### <a name="fault-code-information"></a>Informações de código de falha  
 A tabela a seguir mostra as informações de código de falha XMLA contidas na sessão de detalhe da resposta SOAP. As colunas são os atributos de um erro na seção de detalhe de uma falha SOAP.  
  
|Nome da coluna|Tipo|Description|Nulo permitido<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|**ErrorCode**|**UnsignedInt**|Código de retorno que indica o êxito ou a falha do método. O valor hexadecimal deve ser convertido em um **UnsignedInt** valor.|Não|  
|**WarningCode**|**UnsignedInt**|Código de retorno que indica uma condição de aviso. O valor hexadecimal deve ser convertido em um **UnsignedInt** valor.|Sim|  
|**Description**|**Cadeia de caracteres**|Texto e descrição de erro ou de aviso retornadas pelo componente que gerou o erro.|Sim|  
|**Origem**|**Cadeia de caracteres**|Nome do componente que gerou o erro ou o aviso.|Sim|  
|**Arquivo de ajuda**|**Cadeia de caracteres**|Caminho ou URL para o arquivo de Ajuda ou tópico que descreve o erro ou o aviso.|Sim|  
  
 <sup>1</sup> indica se os dados são necessários e devem ser retornados ou se os dados são opcionais e uma cadeia de caracteres nula será permitida se a coluna não se aplica.  
  
 A seguir, um exemplo de uma falha SOAP ocorrida quando uma chamada de método falhou:  
  
```  
<?xml version="1.0"?>  
   <SOAP-ENV:Envelope  
   xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"  
   SOAP-ENV:encodingStyle="http://schemas.xmlsoap.org/soap/encoding/">  
      <SOAP-ENV:Fault>  
         <faultcode>XMLAnalysisError.0x80000005</faultcode>  
         <faultstring>The XML for Analysis provider encountered an error.</faultstring>  
         <faultactor>XML for Analysis Provider</faultactor>  
         <detail>  
<Error  
ErrorCode="2147483653"  
Description="An unexpected error has occurred."  
Source="XML for Analysis Provider"  
HelpFile="" />  
         </detail>  
      </SOAP-ENV:Fault>  
</SOAP-ENV:Envelope>  
```  
  
##  <a name="handling_errors_and_warnings"></a>Tratamento de erros e avisos  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Retorna o **mensagens** propriedade o **raiz** elemento para um comando se as seguintes situações ocorrerem após a execução do comando:  
  
-   O próprio método não falhou, mas houve uma falha na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] após o êxito da chamada de método.  
  
-   A instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna um aviso quando o comando tem êxito.  
  
 O **mensagens** propriedade segue todas as outras propriedades que são contidas pelo **raiz** elemento e pode conter um ou mais **mensagem** elementos. Por sua vez, cada **mensagem** elemento pode conter um único **erro** ou **aviso** elemento descrevendo erros ou avisos, respectivamente, ocorridos para o comando especificado.  
  
 Para obter mais informações sobre erros e avisos contidos no **mensagens** propriedade, consulte [elemento Messages &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-properties/messages-element-xmla.md).  
  
### <a name="handling-errors-during-serialization"></a>Manipulando erros durante a serialização  
 Se ocorrer um erro após o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância já ter começado a serializar a saída de um comando executado com êxito, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna um [exceção](../../analysis-services/xmla/xml-elements-properties/exception-element-xmla.md) elemento em um namespace diferente no ponto do erro. A instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fechará todos os elementos abertos para que o documento XML enviado ao cliente seja um documento válido. A instância também retornará um **mensagens** elemento que contém a descrição do erro.  
  
##  <a name="handling_inline_errors_and_warnings"></a>Tratamento de erros e avisos embutidos  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Retorna um embutido **erro** ou **aviso** para um comando se o próprio método XMLA não falhou, mas ocorreu um erro específico para um elemento de dados nos resultados retornados pelo método no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância após a chamada de método XMLA foi bem-sucedida.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Fornece **erro** e **aviso** elementos se problemas específicos para uma célula ou outros dados que estão contidos em um **raiz** elemento usando o [ MDDataSet](../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) tipo de dados ocorrem, como um erro de segurança ou formatação de uma célula. Nesses casos, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna um **erro** ou **aviso** elemento o **célula** ou **linha** elemento que contém o erro ou aviso, respectivamente.  
  
 O exemplo a seguir ilustra um conjunto de resultados que contém um erro no conjunto de linhas retornado de um **Execute** usando o método de [instrução](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) comando.  
  
```  
<return>  
   ...  
   <root>  
      ...  
      <CellData>  
      ...  
         <Cell CellOrdinal="10">  
            <Value>  
               <Error>  
                  <ErrorCode>2148497527</ErrorCode>   
                  <Description>Security Error.</Description>   
               </Error>  
            </Value>  
         </Cell>  
      </CellData>  
      ...  
   </root>  
   ...  
</return>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo com XMLA no Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

