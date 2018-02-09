---
title: Propriedade ConnectionString (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::ConnectionString
helpviewer_keywords:
- ConnectionString property [ADO]
ms.assetid: 3be75b75-4d36-4479-ab64-9a456869252a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aaf33c9a4fd5b628307195b9b9a7d1743d24d7f2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="connectionstring-property-ado"></a>Propriedade ConnectionString (ADO)
Indica as informações usadas para estabelecer uma conexão com uma fonte de dados.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor.  
  
## <a name="remarks"></a>Remarks  
 Use o **ConnectionString** propriedade para especificar uma fonte de dados, passando uma cadeia de caracteres de conexão detalhadas que contém uma série de *argumento* *= valor* instruções separadas por ponto e vírgula.  
  
 ADO dá suporte a cinco argumentos para o **ConnectionString** propriedade; qualquer outro passo argumentos diretamente para o provedor sem nenhum processamento pelo ADO. O oferece suporte ao ADO de argumentos são da seguinte maneira.  
  
|Argumento|Description|  
|--------------|-----------------|  
|*Provider=*|Especifica o nome de um provedor a ser usado para a conexão.|  
|*Nome do arquivo =*|Especifica o nome de um arquivo específico do provedor (por exemplo, um objeto de fonte de dados persistentes) que contém informações de conexão predefinidos.|  
|*Provedor remoto =*|Especifica o nome de um provedor a ser usada ao abrir uma conexão de cliente. (Apenas serviço de dados remotos.)|  
|*Remote Server=*|Especifica o nome do caminho do servidor a ser usada ao abrir uma conexão de cliente. (Apenas serviço de dados remotos.)|  
|*URL=*|Especifica a cadeia de caracteres de conexão como uma URL absoluta que identifica um recurso, como um arquivo ou diretório.|  
  
 Depois de definir o **ConnectionString** propriedade e abra o [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) do objeto, o provedor pode alterar o conteúdo da propriedade, por exemplo, mapeando os nomes de argumento definido ADO para seu equivalentes para o provedor específico.  
  
 O **ConnectionString** propriedade herda automaticamente o valor usado para o *ConnectionString* argumento do [abrir](../../../ado/reference/ado-api/open-method-ado-connection.md) método, portanto você pode substituir o atual  **ConnectionString** propriedade durante o **abrir** chamada de método.  
  
 Porque o *nome de arquivo* argumento faz com que o ADO para carregar o provedor associado, você não pode passar ambos o *provedor* e *nome de arquivo* argumentos.  
  
 O **ConnectionString** propriedade é leitura/gravação quando a conexão é fechada e somente leitura quando ela é aberta.  
  
 Duplicatas de um argumento no **ConnectionString** são ignoradas. A última instância de um argumento é usada.  
  
> [!NOTE]
>  **Uso do serviço de dados remoto** quando usado em um cliente **Conexão** objeto, o **ConnectionString** propriedade pode incluir somente o *provedor remoto*e *servidor remoto* parâmetros.  
  
 A tabela a seguir lista o provedor de ADO padrão para cada sistema operacional Windows:  
  
|Provedor de ADO padrão|Sistema operacional Windows|  
|--------------------------|------------------------------|  
|MSDASQL<br /><br /> (Para melhorar a legibilidade do código-fonte, especificar explicitamente o nome do provedor na cadeia de conexão.)|Windows 2000 (32 bits)<br /><br /> Windows XP (32 bits)<br /><br /> Windows 2003 Server (32 bits)<br /><br /> Windows Vista (32 bits)<br /><br /> Windows Vista Service Pack 1 ou posterior (32 bits e 64 bits)<br /><br /> Versões do Windows após o Windows Vista (32 bits e 64 bits)|  
|Nenhum padrão.<br /><br /> Quando um aplicativo ADO é executado nos seguintes sistemas operacionais e não especifica explicitamente o provedor, o ADO retorna o seguinte erro: "ADODB. Conexão: provedor não for especificado e não há nenhum provedor padrão designado "|Windows 2000 (64 bits)<br /><br /> Windows XP (64 bits)<br /><br /> Windows 2003 Server (64 bits)<br /><br /> Windows Vista (64 bits)|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Connection (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de propriedades de estado (VB), ConnectionTimeout e ConnectionString](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [Exemplo de propriedades de estado (VC + +), ConnectionTimeout e ConnectionString](../../../ado/reference/ado-api/connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [Apêndice A: Provedores](../../../ado/guide/appendixes/appendix-a-providers.md)
