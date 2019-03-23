---
title: Formato de pacote do SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: cfe0e5dc-5be3-4222-b721-fe83665edd94
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3b7288952ce9b57b0825f20d1a93fcbcd20d3c37
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374395"
---
# <a name="ssis-package-format"></a>Formato do pacote SSIS
  Na versão atual do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], alterações significativas foram feitas no formato do pacote (arquivo .dtsx) para facilitar a leitura do formato e a comparação dos pacotes. Você também pode mesclar com mais confiança pacotes que não contêm alterações conflitantes ou alterações armazenadas em formato binário.  
  
 Para exibir o formato de arquivo de pacote DTSX atual, consulte [ \[MS-DTSX\]: Especificação de formato de arquivo XML do pacote Data Transformation Services](https://go.microsoft.com/fwlink/?LinkId=233251).  
  
 A lista a seguir detalha as alterações no formato de arquivo: Para exibir exemplos de códigos dessas alterações, consulte [Alterações do formato de pacote no SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=233255).  
  
-   Convenções de formatação foram aplicadas para facilitar a leitura e o entendimento do arquivo .dtsx.  
  
-   O formato é mais conciso. Elementos separados para cada propriedade foram mantidos como atributos, com exceção de PackageFormatVersion. Os atributos são listados alfabeticamente e as propriedades que têm valores padrão não são mais mantidas. Por fim, os elementos que aparecem várias vezes agora estão contidos em um elemento pai.  
  
-   A maioria dos objetos em um pacote que pode ser referenciada por outros objetos agora tem um atributo `refId` definido no XML do pacote. Em vez de manter as IDs de linhagem, a `refID` é mantida agora. IDs de linhagem ainda são usadas no tempo de execução e geradas novamente quando o pacote é carregado.  
  
     O valor `refId` é uma cadeia de caracteres exclusiva legível e compreensível, em comparação com GUIDs ou valores inteiros. A cadeia de caracteres é semelhante aos valores de caminho usados para configurações de pacote nas versões anteriores do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
     Se você estiver mesclando alterações entre duas versões de um pacote, o `refId` poderá ser usado em operações de localizar/substituir para assegurar que todas as referências a esse objeto tenham sido atualizadas corretamente.  
  
-   As informações de layout estão contidas em uma seção CData.  
  
-   As anotações em texto não criptografado são mantidas. Isso facilita a extração das informações para a geração automática da documentação.  
  
  
