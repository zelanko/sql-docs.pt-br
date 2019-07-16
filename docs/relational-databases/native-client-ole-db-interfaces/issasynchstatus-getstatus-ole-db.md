---
title: ISSAsynchStatus::GetStatus (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAsynchStatus::GetStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- GetStatus method
ms.assetid: 354b6ee4-b5a1-48f6-9403-da3bdc911067
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 855bc71e1a7ad7c0d462d16e266f392128b04519
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051022"
---
# <a name="issasynchstatusgetstatus-ole-db"></a>ISSAsynchStatus::GetStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Retorna o status de uma operação que está sendo executada de forma assíncrona.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT GetStatus(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation,  
        DBCOUNTITEM *pulProgress,  
        DBCOUNTITEM *pulProgressMax,  
        DBASYNCHPHASE *peAsynchPhase,  
        LPOLESTR *ppwszStatusText);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hChapter*[in]  
 O identificador do capítulo. Se o objeto que está sendo sondado não for um objeto de conjunto de linhas ou se a operação não se aplicar a um capítulo, esse argumento deverá ser definido como DB_NULL_HCHAPTER, que é ignorado pelo provedor.  
  
 *eOperation*[in]  
 A operação cujo status assíncrono está sendo solicitado. O valor desse argumento deveria ser o seguinte:  
  
 DBASYNCHOP_OPEN – o consumidor solicita informações sobre a abertura ou população assíncrona de um conjunto de linhas ou sobre a inicialização assíncrona de um objeto de fonte de dados. Se o provedor estiver em conformidade com OLE DB 2.5 e der suporte a associação direta de URL, o consumidor solicitará informações sobre a abertura ou população assíncrona de uma fonte de dados, conjunto de linhas, linha ou objeto de fluxo.  
  
 *pulProgress*[out]  
 Um ponteiro de memória no qual retornar o progresso atual da operação assíncrona em relação ao valor máximo esperado do parâmetro *pulProgressMax* . Para obter mais informações sobre o significado de *pulProgress*, consulte a descrição de *peAsynchPhase*.  
  
 Se *pulProgress* for um ponteiro nulo, nenhum progresso será retornado.  
  
 *pulProgressMax*[out]  
 Um ponteiro de memória no qual retornar o valor máximo esperado do parâmetro *pulProgress* . Esse valor pode alterar de uma chamada para outra a este método. Para obter mais informações sobre o significado de *pulProgressMax*, consulte a descrição de *peAsynchPhase*.  
  
 Se *pulProgressMax* for um ponteiro nulo, nenhum valor máximo esperado será retornado.  
  
 *peAsynchPhase*[out]  
 Um ponteiro de memória no qual retornar informações adicionais sobre o progresso da operação assíncrona. Os valores válidos incluem:  
  
 DBASYNCHPHASE_INITIALIZATION – o objeto está em fase de inicialização. Os argumentos *pulProgress* e *pulProgressMax* indicam uma taxa estimada de conclusão. O objeto ainda não se materializou completamente. As tentativas de chamar qualquer outra interface podem falhar e o conjunto completo de interfaces pode não estar disponível no objeto. Se a operação assíncrona tiver sido resultado de uma chamada de **ICommand::Execute** para um comando que atualiza, exclui ou insere linhas e se *cParamSets* for superior a 1, *pulProgress* e *pulProgressMax* podem indicar o progresso de um único conjunto de parâmetros ou da matriz completa de conjuntos de parâmetros.  
  
 DBASYNCHPHASE_POPULATION – o objeto está em fase de rastreamento. Embora o conjunto de linhas esteja totalmente inicializado e a gama completa de interfaces esteja disponível no objeto, talvez ainda haja linhas que não foram populadas no conjunto de linhas. Embora *pulProgress* e *pulProgressMax* possam ser baseados no número de linhas populadas, em geral, eles se baseiam no tempo ou no esforço necessário para popular o conjunto de linhas. Dessa forma, um chamador deveria usar essas informações como uma estimativa aproximada de quanto tempo o processo levaria, não a contagem de linhas eventual. Essa fase só é retornada durante a população de um conjunto de linhas; ela nunca é retornada na inicialização de um objeto de fonte de dados ou pela execução de um comando que atualiza, exclui ou insere linhas.  
  
 DBASYNCHPHASE_COMPLETE – todo o processamento assíncrono do objeto foi concluído. **ISSAsynchStatus::GetStatus** retorna um valor de HRESULT que indica o resultado da operação. Normalmente, esse é o HRESULT que teria sido retornado se a operação tivesse sido chamada de forma síncrona. Se a operação assíncrona foi resultado de uma chamada a **ICommand::Execute** para um comando que atualiza, exclui ou insere linhas, *pulProgress* e *pulProgressMax* têm o mesmo número total de linhas afetadas pelo comando. Se *cParamSets* for maior que 1, esse será o número total de linhas afetadas por todos os conjuntos de parâmetros especificados na execução. Se *peAsynchPhase* for um ponteiro nulo, nenhum código de status será retornado.  
  
 DBASYNCHPHASE_CANCELED – o processamento assíncrono do objeto foi anulado. **ISSAsynchStatus::GetStatus** retorna DB_E_CANCELED. Se a operação assíncrona tiver sido resultado de uma chamada a **ICommand::Execute** para um comando que atualiza, exclui ou insere linhas, *pulProgress* será igual ao número total de linhas, para todos os conjuntos de parâmetros afetados pelo comando antes do cancelamento.  
  
 *ppwszStatusText*[in/out]  
 Um ponteiro de memória que contém informações adicionais sobre a operação. Um provedor pode usar este valor para fazer a distinção entre os elementos de uma operação – por exemplo, recursos diferentes que são acessados. Esta cadeia de caracteres é localizada de acordo com a propriedade DBPROP_INIT_LCID no objeto de fonte de dados.  
  
 Se *ppwszStatusText* for não nulo na entrada, o provedor retornará o status associado ao elemento específico identificado por *ppwszStatusText*. Se *ppwszStatusText* não indicar um elemento de *eOperation*, o provedor retornará S_OK com *pulProgress* e *pulProgressMax* definidos como o mesmo valor. Se o provedor não fizer a distinção entre os elementos com base em um identificador textual, ele definirá *ppwszStatusText* como NULL e retornará informações sobre a operação como um todo; caso contrário, se *ppwszStatusText* for não nulo na entrada, o provedor não irá alterar *ppwszStatusText* .  
  
 Se *ppwszStatusText* for nulo na entrada, o provedor definirá *ppwszStatusText* como um valor que indica mais informações sobre a operação ou como NULL se tais informações não estiverem disponíveis ou se **ISSAsynchStatus::GetStatus** retornar um erro. Quando *ppwszStatusText* for nulo na entrada, o provedor alocará memória para a cadeia de caracteres de status e retornará o endereço a esta memória. O consumidor libera esta memória com **IMalloc::Free** quando ela não precisar mais da cadeia de caracteres.  
  
 Se *ppwszStatusText* for NULL na entrada, nenhuma cadeia de caracteres de status será retornada e o provedor retornará informações sobre qualquer elemento da operação ou sobre a operação em geral.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi retornado com êxito.  
  
-   Se *peAsynchPhase* for igual a DBASYNCHPHASE_INITIALIZATION, é sinal de que o objeto ainda não foi totalmente inicializado; as tentativas de chamar outras interfaces podem falhar e o conjunto completo de interfaces pode não estar disponível no objeto.  
  
-   Se *peAsynchPhase* for igual a DBASYNCHPHASE_POPULATION, é sinal de que o conjunto de linhas foi totalmente inicializado e a gama completa de interfaces está disponível no objeto; no entanto, talvez haja linhas que ainda não tenham sido populadas no conjunto de linhas.  
  
-   Se *peAsynchPhase* for igual a DBASYNCHPHASE_COMPLETE, é sinal de que todo o processamento assíncrono do objeto foi concluído. O objeto está totalmente inicializado e populado.  
  
 DB_E_CANCELED  
 O processamento assíncrono foi cancelado durante a população do conjunto de linhas. O processo de população para, mas o conjunto de linhas permanece válido para as linhas já populadas.  
  
 O processamento assíncrono foi cancelado durante a inicialização do objeto de fonte de dados. O objeto de fonte de dados está em um estado não inicializado.  
  
 E_INVALIDARG  
 O parâmetro *hChapter* está incorreto.  
  
 E_UNEXPECTED  
 **ISSAsynchStatus::GetStatus** foi chamado em um objeto de fonte de dados e **IDBInitialize::Initialize** não foi chamado no objeto de fonte de dados.  
  
 **ISSAsynchStatus::GetStatus** foi chamado em um conjunto de linhas, **ITransaction::Commit** ou **ITransaction::Abort** foi chamado e o objeto está em um estado zumbi.  
  
 **ISSAsynchStatus::GetStatus** foi chamado em um conjunto de linhas cancelado de forma assíncrona em sua fase de inicialização. O conjunto de linhas está em um estado zumbi.  
  
 E_FAIL  
 Ocorreu um erro específico de provedor.  
  
## <a name="remarks"></a>Comentários  
 O método **ISSAsynchStatus::GetStatus** comporta-se exatamente como o método **IDBAsynchStatus::GetStatus**, a não ser pelo fato de que se a inicialização de um objeto de fonte de dados for anulada, E_UNEXPECTED será retornado em vez de DB_E_CANCELED (embora [ISSAsynchStatus::WaitForAsynchCompletion](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) retorne DB_E_CANCELED). Isso acontece porque o objeto de fonte de dados não é deixado no estado normal de zumbi que segue uma operação de anulação, para que outras operações futuras de inicialização possam ser tentadas.  
  
 Se o conjunto de linhas for inicializado ou populado de forma assíncrona, deverá dar suporte a este método.  
  
 Além dos valores de retorno listados, **ISSAsynchStatus::GetStatus** pode retornar qualquer HRESULT que teria sido retornado pelo método que iniciou a operação assíncrona, indicando o êxito ou a falha da operação.  
  
 Algumas operações assíncronas talvez não retornem estados diferentes de "concluído" "não concluído". Elas devem definir *pulProgressMax* como um valor igual a 1, indicando a granularidade “tudo ou nada” de suas estimativas, de modo que suas respostas seriam 0/1 ou 1/1.  
  
 Um provedor pode alterar *pulProgressMax* em chamadas sucessivas e até mesmo retornar uma taxa menor do que a anterior, se isso gerar uma estimativa melhor do grau de conclusão da tarefa.  
  
 O provedor não é obrigado a garantir um nível maior de precisão, mas é incentivado a fazê-lo nos casos em que são possíveis estimativas razoáveis de conclusão. Tais esforços contribuirão para melhorar a qualidade da interface do usuário porque é provável que o uso principal desta função seja fornecer comentários de progresso ao usuário. A satisfação do usuário aumenta com a qualidade dos comentários sobre uma tarefa invisível de longa duração.  
  
 Chamar **ISSAsynchStatus::GetStatus** em um objeto de fonte de dados inicializado ou em um conjunto de linhas populado, ou atribuir um valor a *eOperation* diferente de DBASYNCHOP_OPEN, retorna S_OK com *pulProgress* e *pulProgressMax* definidos como o mesmo valor. Se **ISSAsynchStatus::GetStatus** for chamado em um objeto criado pela execução de um comando que atualiza, exclui ou insere linhas, ambos *pulProgress* e *pulProgressMax* indicam o número total de linhas afetadas pelo comando.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações assíncronas](../../relational-databases/native-client/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
