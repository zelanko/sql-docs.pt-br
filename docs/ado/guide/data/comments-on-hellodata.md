---
title: Comentários sobre o HelloData | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2c4897f82ff8562c031ec3522f47cddebfb56eb2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925802"
---
# <a name="comments-on-hellodata"></a>Comentários sobre o HelloData
O aplicativo HelloData percorre as operações básicas de um aplicativo típico do ADO: Introdução, o exame, edição e atualização de dados. Quando você inicia o aplicativo, clique no botão de primeira **obter dados**. Isso executará o **GetData** sub-rotina.  
  
## <a name="getdata"></a>GetData  
 **GetData** coloca uma cadeia de caracteres de conexão válido em uma variável de nível de módulo *m_sConnStr*. Para obter mais informações sobre cadeias de caracteres de conexão, consulte [criando a cadeia de caracteres de Conexão](../../../ado/guide/data/creating-a-connection-string.md).  
  
 Atribuir um manipulador de erro usando um Visual Basic **OnError** instrução. Para obter mais informações sobre o tratamento de erro no ADO, consulte [tratamento de erro](../../../ado/guide/data/error-handling.md). Uma nova **Conexão** objeto é criado e o **CursorLocation** estiver definida como **adUseClient** porque o HelloData exemplo cria um  *conjunto de registros desconectado*. Isso significa que assim que os dados tiverem sido buscados da fonte de dados, a conexão física com a fonte de dados é interrompida, mas você ainda pode trabalhar com os dados armazenados em cache localmente no seu **Recordset** objeto.  
  
 Depois que a conexão for aberta, atribua uma cadeia de caracteres SQL a uma variável (sSQL). Em seguida, crie uma instância de uma nova **conjunto de registros** objeto, `m_oRecordset1`. Na próxima linha de código, abra o **conjunto de registros** sobre o existente **Conexão**, passando `sSQL` como a origem do **Recordset**. ADO ajudar a tornar a determinação de que a cadeia de caracteres SQL você ter passado como a fonte para o **conjunto de registros** é uma definição textual de um comando, passando **adCmdText** no argumento final para o **Conjunto de registros aberto** método. Essa linha também define o **LockType** e **CursorType** associado com o **conjunto de registros**.  
  
 A próxima linha de código define a **MarshalOptions** propriedade igual a **adMarshalModifiedOnly**. **MarshalOptions** indica quais registros devem ser empacotados para a camada intermediária (ou o servidor Web). Para obter mais informações sobre o marshaling, consulte a documentação do COM. Quando você usa **adMarshalModifiedOnly** com um cursor do lado do cliente ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**), somente os registros que foram modificados no cliente são gravados de volta para a camada intermediária. Definindo **MarshalOptions** à **adMarshalModifiedOnly** pode melhorar o desempenho porque menos linhas têm o marshaling realizadas.  
  
 Em seguida, desconecte o **conjunto de registros** definindo seu **ActiveConnection** propriedade igual a **nada**. Para obter mais informações, consulte a seção "Desconectando e reconectando o conjunto de registros" em [Updating e persistência de dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Feche a conexão à fonte de dados e destruir existente **Conexão** objeto. Isso libera os recursos consumido por ele.  
  
 A etapa final é definir a **conjunto de registros** como o **DataSource** para a grade de dados do Microsoft de controle no formulário até que você pode facilmente exibir os dados do **conjunto de registros** no formulário.  
  
 Clique no botão segunda **examinar dados**. Isso executa o **ExamineData** sub-rotina.  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData usa vários métodos e propriedades do **conjunto de registros** objeto para exibir informações sobre os dados no **conjunto de registros**. Ele informa o número de registros usando o **RecordCount** propriedade. Ele percorre o **conjunto de registros** e imprime o valor da **AbsolutePosition** propriedade na caixa de texto de exibição no formulário. Também enquanto estiver no loop, o valor da **indicador** propriedade para o terceiro registro é colocada em uma variável de variant *vBookmark*, para uso posterior.  
  
 A rotina diretamente navega de volta para o terceiro registro usando a variável de indicador que ele armazenou anteriormente. As chamadas de rotina a **WalkFields** sub-rotina, que percorre a **campos** coleção da **conjunto de registros** e exibe detalhes sobre cada **campo**  na coleção.  
  
 Por fim, **ExamineData** usa o **filtro** propriedade do **conjunto de registros** a tela para somente os registros com um **CategoryId** igual a 2. O resultado de aplicar esse filtro é imediatamente visível na grade de exibição no formulário.  
  
 Para obter mais informações sobre a funcionalidade que mostra a **ExamineData** sub-rotina, consulte [examinando dados](../../../ado/guide/data/examining-data.md).  
  
 Em seguida, clique no botão terceiro **editar dados**. Isso executará o **EditData** sub-rotina.  
  
## <a name="editdata"></a>EditData  
 Quando o código entra o **EditData** sub-rotina, o **conjunto de registros** ainda é filtrada no **CategoryId** igual a 2, para que somente os itens que atendem aos critérios de filtro visível. Primeiro percorre os **conjunto de registros** e aumenta o preço de cada item visível na **conjunto de registros** em 10 por cento. O valor da **Price** campo é alterado Configurando a **valor** propriedade desse campo igual ao valor de um novo, válido.  
  
 Lembre-se de que o **Recordset** está desconectado da fonte de dados. As alterações que foram feitas na **EditData** são feitas apenas para a cópia localmente em cache dos dados. Para obter mais informações, consulte [editando dados](../../../ado/guide/data/editing-data.md).  
  
 As alterações não serão feitas na fonte de dados até que você clique no botão quarto **atualização de dados**. Isso executará o **UpdateData** sub-rotina.  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData primeiro remove o filtro que foi aplicado para o **conjunto de registros**. Remove o código e a redefine `m_oRecordset1` como o **fonte de dados** para a Microsoft associado DataGrid no formulário para que o não filtrado **conjunto de registros** aparece na grade.  
  
 O código, em seguida, verifica para ver se é possível mover para trás **conjunto de registros** usando o **dá suporte à** método com o **adMovePrevious** argumento.  
  
 A rotina move para o primeiro registro usando o **MoveFirst** método e exibe os valores do campo original e atual, usando o **OriginalValue** e **valor** Propriedades do **campo** objeto. Essas propriedades, juntamente com o **UnderlyingValue** propriedade (não usado aqui), são discutidos em [atualizando e persistência de dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Em seguida, uma nova **Conexão** objeto é criado e usado para restabelecer uma conexão à fonte de dados. Você se reconectar a **conjunto de registros** à fonte de dados, definindo a nova **Conexão** como o **ActiveConnection** para o **Recordset**. Para enviar as atualizações para o servidor, o código chama **UpdateBatch** sobre o **conjunto de registros**.  
  
 Se a atualização em lotes for bem-sucedida, uma variável de sinalizador de nível de módulo, `m_flgPriceUpdated`, está definido como True. Isso o lembrará mais tarde para limpar todas as alterações que foram feitas no banco de dados.  
  
 Por fim, o código de volta para o primeiro registro na **Recordset** e exibe os valores originais e atuais. Os valores são os mesmos após a chamada para **UpdateBatch**.  
  
 Para obter informações detalhadas sobre como atualizar dados, incluindo o que fazer quando dados sobre as alterações de servidor ao seu **conjunto de registros** é desconectado, consulte [atualizando e persistência de dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
## <a name="formunload"></a>Form_Unload  
 O **Form_Unload** sub-rotina é importante por vários motivos. Em primeiro lugar, como esse é um aplicativo de exemplo, Form_Unload limpa as alterações que foram feitas no banco de dados antes de sair do aplicativo. Em segundo lugar, o código mostra como um comando pode ser executado diretamente de um aberto **Conexão** objeto usando o **Execute** método. Por fim, ele mostra um exemplo de como executar uma consulta não retornam linhas (uma consulta de atualização) na fonte de dados.
