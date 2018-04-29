---
title: Propriedades personalizadas OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 13a82d41-dd7a-4708-bc84-4407a536c877
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ce22060489349bf270ef3668236cc5d4f09e4aac
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="ole-db-custom-properties"></a>Propriedades personalizadas OLE DB
  **Propriedades personalizadas de fontes**  
  
 A origem OLE DB tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da origem de OLE DB. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|O modo usado para acessar o banco de dados. Os valores possíveis são **Abrir Conjunto de Linhas**, **Abrir Conjunto de Linhas da Variável**, **Comando do SQL**e **Comando SQL da Variável**. O valor padrão é **Abrir Conjunto de Linhas**.|  
|AlwaysUseDefaultCodePage|Booliano|Um valor que indica se o valor da propriedade **DefaultCodePage** deve ser usado para todas as colunas ou para tentar derivar a página de código da localidade de cada coluna. O valor padrão dessa propriedade é **False**.|  
|CommandTimeOut|Integer|O número de segundos antes de um comando expirar. Um valor de 0 indica que nunca expirará.<br /><br /> Observação: essa propriedade não está disponível no **Editor de Origem OLE DB**, mas pode ser definida usando o **Editor Avançado**.|  
|DefaultCodePage|Integer|A página de código a ser usada quando informações de página de código não estão disponíveis na fonte de dados.|  
|OpenRowset|Cadeia de caracteres|O nome do objeto de banco de dados usado para abrir um conjunto de linhas.|  
|OpenRowsetVariable|Cadeia de caracteres|A variável que contém o nome do objeto de banco de dados usado para abrir um conjunto de linhas.|  
|ParameterMapping|Cadeia de caracteres|O mapeamento de parâmetros no comando SQL para variáveis.|  
|SqlCommand|Cadeia de caracteres|O comando SQL a ser executado.|  
|SqlCommandVariable|Cadeia de caracteres|A variável que contém o comando do SQL a ser executado.|  
  
 A saída e as colunas de saída da origem OLE DB não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [OLE DB Source](../../integration-services/data-flow/ole-db-source.md).  
  
 **Propriedades personalizadas de destino**  
  
 O destino OLE DB tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino OLE DB. Todas as propriedades são de leitura/gravação.  
  
> [!NOTE]  
>  As opções de FastLoad listadas aqui (FastLoadKeepIdentity, FastLoadKeepNulls e FastLoadOptions) correspondem às propriedades de nomes parecidas expostas pela interface **IRowsetFastLoad** implementada pelo Provedor Microsoft OLE DB para SQL Server (SQLOLEDB). Para obter mais informações, procure por IRowsetFastLoad na Biblioteca MSDN.  
  
|Nome da propriedade|Tipo de Dados|Description|  
|-------------------|---------------|-----------------|  
|AccessMode|Inteiro (enumeração)|Um valor que especifica como o destino acessa o seu banco de dados de destino.<br /><br /> Essa propriedade pode ter um dos seguintes valores:<br /><br /> <br /><br /> **OpenRowset** (0) – Forneça o nome de uma tabela ou exibição.<br /><br /> **OpenRowset from Variable** (1) – Forneça o nome de uma variável que contém o nome de uma tabela ou exibição.<br /><br /> **OpenRowset Using Fastload** (3) – Forneça o nome de uma tabela ou exibição.<br /><br /> **OpenRowset Using Fastload from Variable** (4) – Forneça o nome de uma variável que contém o nome de uma tabela ou exibição.<br /><br /> **Comando SQL** (2) – Forneça uma instrução SQL.|  
|AlwaysUseDefaultCodePage|Booliano|Um valor que indica se o valor da propriedade **DefaultCodePage** deve ser usado para todas as colunas ou para tentar derivar a página de código da localidade de cada coluna. O valor padrão dessa propriedade é **False**.|  
|CommandTimeOut|Integer|O número máximo de segundos em que o comando SQL pode ser executado antes que o tempo limite seja excedido. O valor 0 indica que não há limite de tempo. O valor padrão dessa propriedade é 0.<br /><br /> Observação: essa propriedade não está disponível no **Editor de Destinos OLE DB**, mas pode ser definida no **Editor Avançado**.|  
|DefaultCodePage|Integer|A página de código padrão associada ao destino OLE DB.|  
|FastLoadKeepIdentity|Booliano|Um valor que especifica se os valores de identidade devem ser copiados quando os dados são carregados. Essa propriedade só está disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é **False**. Essa propriedade corresponde à propriedade [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) do OLE DB **SSPROP_FASTLOADKEEPIDENTITY**.|  
|FastLoadKeepNulls|Booliano|Um valor que especifica se os valores Nulos devem ser copiados quando os dados são carregados. Essa propriedade só está disponível com uma das opções de carregamento rápido. O valor padrão dessa propriedade é **False**. Essa propriedade corresponde à propriedade [IRowsetFastLoad &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) do OLE DB **SSPROP_FASTLOADKEEPNULLS**.|  
|FastLoadMaxInsertCommitSize|Integer|Um valor que especifica o tamanho do lote que o destino OLE DB tenta confirmar durante as operações de carregamento rápido. O valor padrão, **0**, indica uma única operação de confirmação após o processamento de todas as linhas.|  
|FastLoadOptions|Cadeia de caracteres|Uma coleção de opções de carregamento rápido. As opções de carregamento rápido incluem o bloqueio de tabelas e a verificação de restrições. É possível especificar uma, ambas ou nenhuma. Essa propriedade corresponde à propriedade IRowsetFastLoad do OLE DB **SSPROP_FASTLOADOPTIONS** e aceita opções de cadeia de caracteres como **CHECK_CONSTRAINTS** e **TABLOCK**.<br /><br /> Observação: algumas opções dessa propriedade não estão disponíveis no **Editor de Destinos do Excel**, mas podem ser definidas no **Editor Avançado**.|  
|OpenRowset|Cadeia de caracteres|Quando AccessMode é **OpenRowset**, o nome da tabela ou exibição acessada pelo destino OLE DB.|  
|OpenRowsetVariable|Cadeia de caracteres|Quando AccessMode é **OpenRowset from Variable**, o nome da variável que contém o nome da tabela ou exibição acessada pelo destino OLE DB.|  
|SqlCommand|Cadeia de caracteres|Quando AccessMode é **Comando SQL**, a instrução Transact-SQL usada pelo destino OLE DB para especificar as colunas de destino dos dados.|  
  
 A entrada e as colunas de entrada do destino OLE DB não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [OLE DB Destination](../../integration-services/data-flow/ole-db-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
