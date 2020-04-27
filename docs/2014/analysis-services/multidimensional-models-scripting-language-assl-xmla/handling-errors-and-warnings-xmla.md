---
title: Tratamento de erros e avisos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 856886a5edfa5dcae604b44f5c2dca356ba0addb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62702130"
---
# <a name="handling-errors-and-warnings-xmla"></a>Manipulando erros e avisos (XMLA)
  O tratamento de erros é necessário quando uma chamada de método [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) ou [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) de XML for Analysis (XMLA) não é executada, é executada com êxito, mas gera erros ou avisos ou é executada com êxito, mas retorna resultados que contêm erros.  
  
|Erro|Relatórios|  
|-----------|---------------|  
|A chamada de método XMLA não é executada|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna uma mensagem de falha SOAP que contém os detalhes da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] falha.<br /><br /> Para obter mais informações, consulte a seção [manipulando falhas de SOAP](#handling_soap_faults).|  
|Erros ou avisos em uma chamada de método com êxito|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]inclui um elemento [Error](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) ou [Warning](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/warning-element-xmla) para cada erro ou aviso, respectivamente, na propriedade [messages](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla) do elemento [raiz](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) que contém os resultados da chamada de método.<br /><br /> Para obter mais informações, consulte a seção [Manipulando erros e avisos](#handling_errors_and_warnings).|  
|Erros no resultado de uma chamada de método com êxito|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]inclui um elemento `error` embutido ou `warning` para o erro ou aviso, respectivamente, dentro da [célula](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla) ou elemento de [linha](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/row-element-xmla) apropriado dos resultados da chamada de método.<br /><br /> Para obter mais informações, consulte a seção [Manipulando erros e avisos embutidos](#handling_inline_errors_and_warnings).|  
  
##  <a name="handling-soap-faults"></a><a name="handling_soap_faults"></a>Manipulando falhas de SOAP  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna uma falha SOAP quando ocorrem as seguintes situações:  
  
-   A mensagem SOAP que contém o método XMLA não foi bem formada ou não pôde ser validada pela instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Houve um erro de comunicação ou outro erro envolvendo a mensagem SOAP que contém o método XMLA.  
  
-   O método XMLA não foi executado na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Os códigos de falha SOAP para XMLstartA começam com "XMLForAnalysis", seguido por um ponto e o código de resultado hexadecimal HRESULT. Por exemplo, um código de erro "`0x80000005`" é formatado como "`XMLForAnalysis.0x80000005`". Para obter mais informações sobre o formato de falha SOAP, consulte Falha Soap no protocolo SOAP 1.1 do W3C.  
  
### <a name="fault-code-information"></a>Informações de código de falha  
 A tabela a seguir mostra as informações de código de falha XMLA contidas na sessão de detalhe da resposta SOAP. As colunas são os atributos de um erro na seção de detalhe de uma falha SOAP.  
  
|Nome da coluna|Tipo|Descrição|Nulo permitido<sup>1</sup>|  
|-----------------|----------|-----------------|------------------------------|  
|`ErrorCode`|`UnsignedInt`|Código de retorno que indica o êxito ou a falha do método. O valor hexadecimal deve ser convertido para um valor `UnsignedInt`.|Não|  
|`WarningCode`|`UnsignedInt`|Código de retorno que indica uma condição de aviso. O valor hexadecimal deve ser convertido para um valor `UnsignedInt`.|Sim|  
|`Description`|`String`|Texto e descrição de erro ou de aviso retornadas pelo componente que gerou o erro.|Sim|  
|`Source`|`String`|Nome do componente que gerou o erro ou o aviso.|Sim|  
|`HelpFile`|`String`|Caminho ou URL para o arquivo de Ajuda ou tópico que descreve o erro ou o aviso.|Sim|  
  
 <sup>1</sup> indica se os dados são obrigatórios e devem ser retornados, ou se os dados são opcionais, e se a coluna não se aplica.  
  
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
  
##  <a name="handling-errors-and-warnings"></a><a name="handling_errors_and_warnings"></a>Manipulando erros e avisos  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retornará a propriedade `Messages` no elemento `root` para um comando se as situações a seguir ocorrerem após a execução do comando:  
  
-   O próprio método não falhou, mas houve uma falha na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] após o êxito da chamada de método.  
  
-   A instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna um aviso quando o comando tem êxito.  
  
 A propriedade `Messages` segue todas as outras propriedades contidas pelo elemento `root` e pode conter um ou mais elementos `Message`. Por sua vez, cada elemento `Message` pode conter um único elemento `error` ou `warning` descrevendo erros ou avisos, respectivamente, ocorridos para o comando especificado.  
  
 Para obter mais informações sobre erros e avisos contidos na `Messages` Propriedade, consulte [elemento messages &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/messages-element-xmla).  
  
### <a name="handling-errors-during-serialization"></a>Manipulando erros durante a serialização  
 Se ocorrer um erro depois que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a instância já tiver começado a serializar a saída de um comando de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] execução bem-sucedida, o retornará um elemento de [exceção](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/exception-element-xmla) em um namespace diferente no ponto do erro. A instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fechará todos os elementos abertos para que o documento XML enviado ao cliente seja um documento válido. A instância também retornará um elemento `Messages` com a descrição do erro.  
  
##  <a name="handling-inline-errors-and-warnings"></a><a name="handling_inline_errors_and_warnings"></a>Manipulando erros e avisos embutidos  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retornará um `error` ou `warning` embutido para um comando se o próprio método XMLA não tenha falhado, mas houve um erro específico de um elemento de dados nos resultados retornados pelo método na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] após o êxito da chamada de método XMLA.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]fornece elementos `error` embutidos e `warning` se problemas específicos a uma célula ou a outros dados contidos em um `root` elemento usando o tipo de dados [MDDataSet](https://docs.microsoft.com/bi-reference/xmla/xml-data-types/mddataset-data-type-xmla) ocorrem, como um erro de segurança ou erro de formatação para uma célula. Nesses casos, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna um elemento `error` ou `warning` no elemento `Cell` ou `row` que contém o erro ou o aviso, respectivamente.  
  
 O exemplo a seguir ilustra um conjunto de resultados que contém um erro no conjunto de linhas `Execute` retornado de um método usando o comando de [instrução](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
