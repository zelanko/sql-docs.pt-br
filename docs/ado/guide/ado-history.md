---
title: Histórico de ADO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a84ccbb97c26ea92f31212933aac79bde2784b72
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67927163"
---
# <a name="ado-features-for-each-release"></a>Recursos do ADO para cada versão

Este tópico lista os novos recursos introduzidos por cada versão do ADO, ADO MD e ADOX.

## <a name="ado-60"></a>ADO 6,0

 O ADO 6,0 está incluído no Windows Vista, como parte dos componentes de acesso a dados do Windows (DAC do Windows) 6,0. O ADO 6,0 é funcionalmente equivalente ao ADO 2,8.

## <a name="ado-28"></a>ADO 2,8

 O ADO 2,8 foi incluído no Windows XP e no Windows Server 2003, como parte do MDAC (Microsoft Data Access Components) 2,8. Uma versão redistribuível do MDAC 2,8 também está disponível; Observe que essa versão redistribuível só deve ser instalada no Windows 2000. O ADO 2,8 resolve várias preocupações relacionadas à segurança:

 *O acesso ao disco rígido não é permitido fora de uma zona confiável.*
Em scripts entre domínios que envolvem sites não confiáveis, as seguintes operações são desabilitadas: **Stream. SaveToFile**, **Stream. LoadFromFile**, **Recordset. Save**e **Recordset. Open**, usados em conjunto com o sinalizador **AdCmdFile** ou com o MSPersist (Microsoft OLE DB Persistence Provider).

 **Recordset. Open** _,_  **Recordset. Save** _,_  **Stream. SaveToFile** _e_  **Stream. loaddofile**  _operam somente em arquivos físicos._
Esses métodos agora verificam se os identificadores de arquivo apontam somente para arquivos físicos.

 **Recordset. ActiveCommand**  _retorna um erro quando invocado de uma página HTML/ASP._
Isso impede que o objeto de **comando** seja usado inapropriadamente.

 _O número de_**conjuntos de registros**_retornados por um comando de forma aninhada_**Shape**_tem um limite superior._        
Um comando Shape aninhado agora retorna um máximo de 512 **conjuntos de registros**. Isso significa que um comando de **forma** não pode mais ser aninhado em qualquer profundidade. Em vez disso, a profundidade máxima de nível é 512, se cada comando resultar em um único **conjunto de registros**(filho). Se, em qualquer nível, um comando de **forma** retornar vários **conjuntos de registros**, o nível máximo de profundidade será menor que 512.

## <a name="ado-27"></a>ADO 2,7

 *suporte à plataforma de 64 bits* O ADO 2,7 apresenta suporte para processadores de 64 bits.

## <a name="ado-26"></a>ADO 2,6

 O_método_ **CubDef. GetSchemaObject**a partir do ADO 2,6, ADO MD objetos podem ser recuperados usando nomes exclusivos, conforme especificado pela [Propriedade UniqueName (ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md).   Os nomes dos objetos pai não precisam ser conhecidos e as coleções pai não precisam ser preenchidas para recuperar um objeto de esquema. Consulte [Método GetSchemaObject (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md).

 *Fluxos de comando* O objeto **Command** dá suporte a comandos no formato de fluxo como uma alternativa ao uso da propriedade **CommandText** . A [propriedade CommandStream (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md) pode ser usada para especificar modelos XML ou Updategrams como a entrada de **comando** com o provedor de OLE DB da Microsoft para SQL Server.

 O [dialeto](../../ado/reference/ado-api/dialect-property.md) da_Propriedade_ **Dialect**é uma nova propriedade que define a sintaxe e as regras gerais que o provedor usa para analisar a cadeia de caracteres ou o fluxo.  

 _Método_ **Command. Execute**o [método execute](../../ado/reference/ado-api/execute-method-ado-command.md) do objeto de **comando** ADO foi aprimorado para usar fluxos para entrada e saída.  

 *Statusvalues de campo* Se o usuário encontrar um erro de DB_E_ERRORSOCCURRED ao modificar um **campo** de um **conjunto de registros**, o ADO agora preencherá a propriedade **Field. status** com as informações de status apropriadas, de modo que o usuário terá mais informações sobre o que deu errado. Consulte [Propriedade Status (campo ADO)](../../ado/reference/ado-api/status-property-ado-field.md).

 A propriedade **nomeadaparameters**_property_ [chamadaparameters](../../ado/reference/ado-api/namedparameters-property-ado.md) é uma nova propriedade do objeto de **comando** que indica que o provedor deve usar parâmetros nomeados.  

 *Conjuntos de resultados em fluxos* O ADO pode retornar ResultSets de uma fonte de dados em um **fluxo**, em vez de um objeto **Recordset** . Usando a versão mais recente do provedor de OLE DB da Microsoft para SQL Server, você pode obter resultados XML do provedor executando uma consulta "for XML". Um **fluxo** que recebe o ResultSet pode ser aberto com um comando "for XML" como a origem. Consulte [recuperando conjuntos de resultados em fluxos](../../ado/guide/data/retrieving-resultsets-into-streams.md).

 *ResultSet de linha única* O objeto de **registro** ADO agora pode ser aberto em uma cadeia de caracteres de comando ou objeto de **comando** que retorna uma linha de dados do provedor. Isso resulta em um desempenho aprimorado com provedores MDAC 2,6. Consulte o [método Open (registro ADO)](../../ado/reference/ado-api/open-method-ado-record.md).

## <a name="ado-25"></a>ADO 2,5

 O _objeto_ de **registro** ADO 2,5 apresenta o objeto **Record** para representar e gerenciar uma linha de um **conjunto de registros** ou de um provedor de dados, ou um objeto encapsulando dados semiestruturados, como um arquivo ou diretório.

 O _objeto_ de **fluxo** ADO 2,5 também apresenta o objeto de **fluxo** para representar um fluxo de dados binários ou de texto.

 *Associação de URL* O ADO 2,5 apresenta o uso de uma URL, como uma alternativa a uma cadeia de conexão e texto de comando, para nomear objetos de armazenamento de dados. Uma URL pode ser usada com os objetos de **conexão** e **conjunto de registros** existentes, bem como com os novos objetos de **registro** e de **fluxo** .

 *Provedores de dados com suporte para associação de URL* O ADO 2,5 dá suporte a provedores de OLE DB que reconhecem os esquemas de URL. Isso inclui o provedor de OLE DB para publicação na Internet, que acessa o sistema de arquivos do Windows 2000 e reconhece o esquema HTTP existente.
