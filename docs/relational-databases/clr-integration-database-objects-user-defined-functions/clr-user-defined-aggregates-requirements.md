---
title: Requisitos para agregações CLR definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- aggregate functions [CLR integration]
- user-defined types [CLR integration], user-defined aggregates
- CREATE AGGREGATE statement
- SqlUserDefinedAggregate attribute
- aggregate methods [CLR integration]
- assemblies [CLR integration], user-defined aggregate functions
- custom aggregates [CLR integration]
- user-defined functions [CLR integration]
- UDTs [CLR integration], user-defined aggregates
ms.assetid: dbf9eb5a-bd99-42f7-b275-556d0def045d
caps.latest.revision: 56
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: dd8835f9468179f412c1d0857426c93fa5663495
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37356188"
---
# <a name="clr-user-defined-aggregates---requirements"></a>Agregações definidas pelo usuário CLR - requisitos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Um tipo em um assembly do CLR pode ser registrado como uma função de agregação definida pelo usuário, desde que implemente o contrato de agregação necessário. Esse contrato consiste as **SqlUserDefinedAggregate** métodos de contrato de atributo e a agregação. O contrato de agregação inclui o mecanismo para salvar o estado intermediário da agregação e o mecanismo para acumular novos valores, que consiste em quatro métodos: **Init**, **Accumulate**,  **Mesclar**, e **encerrar**. Quando você tiver atendido esses requisitos, você poderá aproveitar ao máximo de agregações definidas pelo usuário no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As seguintes seções deste tópico fornecem detalhes adicionais sobre como criar e trabalhar com agregações definidas pelo usuário. Por exemplo, consulte [funções de agregação Invoking CLR User-Defined](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md).  
  
## <a name="sqluserdefinedaggregate"></a>SqlUserDefinedAggregate  
 Para obter mais informações, consulte [SqlUserDefinedAggregateAttribute](http://go.microsoft.com/fwlink/?LinkId=124626).  
  
## <a name="aggregation-methods"></a>Métodos de agregação  
 A classe registrada como uma agregação definida pelo usuário deve dar suporte aos seguintes métodos de instância. Eles são os métodos que o processador de consultas usa para computar a agregação:  
  
|Método|Sintaxe|Description|  
|------------|------------|-----------------|  
|**Init**|`public void Init();`|O processador de consultas usa esse método para inicializar a computação da agregação. Ele é invocado uma vez para cada grupo que o processador de consultas está agregando. O processador de consultas pode optar por reutilizar a mesma instância da classe de agregação para computar agregações de grupos vários. O **Init** método deve executar qualquer limpeza conforme a necessidade de usos anteriores desta instância e habilitá-lo para iniciar novamente uma nova computação da agregação.|  
|**Acumular**|`public void Accumulate ( input-type value[, input-type value, ...]);`|Um ou mais parâmetros que representam os parâmetros da função. *input_type* deve ser gerenciado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados equivalente ao nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados especificado por *input_sqltype* no **CREATE AGGREGATE** instrução. Para obter mais informações, consulte [Mapeando dados de parâmetro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).<br /><br /> Para UDTs (tipos definidos pelo usuário), o tipo de entrada é o mesmo que o tipo do UDT. O processador de consultas usa esse método para acumular os valores de agregação. Ele é invocado uma vez para obter cada valor no grupo que está sendo agregado. O processador de consultas sempre chama somente depois de chamar o **Init** método em determinada instância da classe agregação. A implementação desse método deve atualizar o estado da instância para refletir o acúmulo do valor do argumento que é passado.|  
|**Mesclagem**|`public void Merge( udagg_class value);`|Esse método pode ser usado para mesclar outra instância desta classe de agregação com a instância atual. O processador de consultas usa esse método para mesclar várias computações parciais de uma agregação.|  
|**Encerrar**|`public return_type Terminate();`|Esse método completa a computação de agregações e retorna o resultado da agregação. O *return_type* deve ser gerenciado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados que é o equivalente gerenciado *return_sqltype* especificado no **CREATE AGGREGATE** instrução. O *return_type* também pode ser um tipo definido pelo usuário.|  
  
### <a name="table-valued-parameters"></a>Parâmetros com valor de tabela  
 Os TVPs (parâmetros com valor de tabela), ou seja, tipos de tabela definidos pelo usuário transmitidos para um procedimento ou uma função, oferecem uma maneira eficiente de passar várias linhas de dados para o servidor. Os TVPs proporcionam funcionalidade semelhante para matrizes de parâmetro, porém com maior flexibilidade e integração com [!INCLUDE[tsql](../../includes/tsql-md.md)]. Eles também fornecem o potencial para melhor desempenho. Os TVPs também ajudam a reduzir o número de viagens de ida e volta para o servidor. Em vez de enviar várias solicitações ao servidor, como com uma lista de parâmetros escalares, os dados podem ser enviados ao servidor como um TVP. Um tipo de tabela definido pelo usuário não pode ser passado como um parâmetro com valor de tabela para, ou ser retornado de, um procedimento armazenado ou uma função gerenciada(o) que é executada(o) no processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Além disso, TVPs não podem ser usados dentro do escopo de uma conexão de contexto. Entretanto, um TVP pode ser usado com o SqlClient nos procedimentos armazenados gerenciados ou nas funções em execução no processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se for usado em uma conexão que não seja de contexto. A conexão pode ser com o mesmo servidor que está executando o procedimento ou função gerenciada. Para obter mais informações sobre TVPs, consulte [usar parâmetros &#40;mecanismo de banco de dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Atualizada a descrição do **Accumulate** método; ele agora aceita mais de um parâmetro.|  
  
## <a name="see-also"></a>Consulte também  
 [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [Invocando funções de agregação CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregate-invoking-functions.md)  
  
  
