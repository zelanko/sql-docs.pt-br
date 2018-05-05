---
title: Histórico de ADO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, what's new
ms.assetid: 667673f2-3151-432b-894a-3fc60b704ea4
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc6116c80af9ae7ca6a6504a1caa2d912b0d3731
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="ado-features-for-each-release"></a>Recursos do ADO para cada versão.
Este tópico lista os novos recursos introduzidos por cada versão do ADO MD, ADO e ADOX.

## <a name="ado-60"></a>ADO 6.0
 ADO 6.0 está incluído no Windows Vista, como parte do Windows Data Access Components (Windows DAC) 6.0. ADO 6.0 é funcionalmente equivalente ao ADO 2.8.

## <a name="ado-28"></a>ADO 2.8
 ADO 2.8 foi incluído no Windows XP e Windows Server 2003, como parte do Microsoft Data Access Components (MDAC) 2.8. Uma versão redistribuível do MDAC 2.8 também está disponível. Observe que esta versão redistribuível só deve ser instalado no Windows 2000. ADO 2.8 aborda várias questões relacionadas à segurança:

 *Acesso de unidade de disco rígido não é permitido fora de uma zona confiável.*
No domínio cruzado script envolvendo sites não confiáveis, as operações a seguir estão desabilitadas: **Stream.SaveToFile**, **Stream.LoadFromFile**, **Recordset.Save**, e **Recordset.Open**, usado em conjunto com o **adCmdFile** sinalizador ou com o Microsoft OLE DB provedor de persistência (MSPersist).

 **Recordset.Open** *,***Recordset.Save** *,***Stream.SaveToFile** *, e* **Stream.LoadFromFile***operar somente arquivos físicos.*
Esses métodos agora verificar o ponto de identificadores de arquivo para arquivos físicos apenas.

 **Recordset.ActiveCommand***retorna um erro quando chamado a partir de uma página HTML/ASP.*
Isso impede que o **comando** objeto sejam mal utilizadas.

 *O número de***conjuntos de registros***retornado por uma instrução***forma***comando possui um limite superior.*
Um comando de forma aninhada agora retorna um máximo de 512 **conjuntos de registros**. Isso significa que um **forma** comando não pode ser aninhado em qualquer profundidade. Em vez disso, a profundidade máxima de nível é 512, se cada comando resulta em uma única (filho) **registros**. Se, em qualquer nível, um **forma** comando retorna várias **conjuntos de registros**, o nível máximo de profundidade será menor que 512.

## <a name="ado-27"></a>ADO 2.7
 *suporte a plataformas de 64 bits* ADO 2.7 introduz suporte para processadores de 64 bits.

## <a name="ado-26"></a>ADO 2.6
 **CubDef.GetSchemaObject***método* começando com o ADO 2.6, objetos do ADO MD podem ser recuperados usando nomes exclusivos, conforme especificado pelo [propriedade UniqueName (ADO MD)](../../ado/reference/ado-md-api/uniquename-property-ado-md.md). Os nomes de objetos pai não precisam ser conhecidos e coleções pai não precisam ser preenchidos para recuperar um objeto de esquema. Consulte [GetSchemaObject método (ADO MD)](../../ado/reference/ado-md-api/getschemaobject-method-ado-md.md).

 *Comando fluxos* o **comando** objeto dá suporte a comandos no formato de fluxo como uma alternativa ao uso de **CommandText** propriedade. O [propriedade CommandStream (ADO)](../../ado/reference/ado-api/commandstream-property-ado.md) pode ser usado para especificar modelos XML ou diagramas de atualização como o **comando** de entrada com o Microsoft OLE DB Provider para SQL Server.

 **Dialeto***propriedade* [dialeto](../../ado/reference/ado-api/dialect-property.md) é uma nova propriedade que define a sintaxe e geral de regras que o provedor usa para analisar a cadeia de caracteres ou fluxo.

 **Command.Execute***método* o [executar o método](../../ado/reference/ado-api/execute-method-ado-command.md) de ADO **comando** objeto foi aprimorado para usar fluxos de entrada e saída.

 *Campo statusvalues* se o usuário encontra um erro DB_E_ERRORSOCCURRED ao modificar um **campo** de um **registros**, ADO preencherá o **Field.Status**propriedade com as informações de status apropriado para que o usuário tenha mais informações sobre o que deu errado. Consulte [a propriedade de Status (campo ADO)](../../ado/reference/ado-api/status-property-ado-field.md).

 **NamedParameters***propriedade* [NamedParameters](../../ado/reference/ado-api/namedparameters-property-ado.md) é uma nova propriedade do **comando** chamado de objeto que indica que o provedor deve usar parâmetros.

 *Conjuntos de resultados em fluxos* ADO pode retornar conjuntos de resultados de uma fonte de dados em um **fluxo**, em vez de **registros** objeto. Usando a versão mais recente do Microsoft OLE DB Provider para SQL Server, você pode obter resultados XML do provedor executando uma consulta de "Para XML". Um **fluxo** que recebe o conjunto de resultados pode ser aberto com um comando "Para XML" como a origem. Consulte [recuperar conjuntos de resultados em fluxos](../../ado/guide/data/retrieving-resultsets-into-streams.md).

 *Conjunto de resultados de linha única* o ADO **registro** objeto agora pode ser aberto em uma cadeia de caracteres de comando ou **comando** objeto que retorna uma linha de dados do provedor. Isso resulta em desempenho aprimorado com provedores MDAC 2.6. Consulte [(registro de ADO) do método Open](../../ado/reference/ado-api/open-method-ado-record.md).

## <a name="ado-25"></a>ADO 2.5
 **Registro** *objeto* ADO 2.5 apresenta o **registro** objeto para representar e gerenciar uma linha de um **registros** ou um provedor de dados ou um objeto que encapsula um dados estruturados, como um arquivo ou diretório.

 **Fluxo** *objeto* ADO 2.5 também apresenta o **fluxo** objeto para representar um fluxo de dados binários ou de texto.

 *Associação de URL* ADO 2.5 apresenta o uso de uma URL, como uma alternativa para uma conexão comando e cadeia de caracteres de texto, para nomear objetos do repositório de dados. Uma URL pode ser usada com a existente **Conexão** e **registros** objetos, bem como com o novo **registro** e **fluxo** objetos.

 *Provedores de dados com suporte a associação de URL* ADO 2.5 dá suporte a provedores OLE DB que reconhecem os esquemas de URL. Isso inclui o provedor OLE DB para publicação de Internet, que acessa o sistema de arquivos do Windows 2000 e reconhece o esquema HTTP existente.
