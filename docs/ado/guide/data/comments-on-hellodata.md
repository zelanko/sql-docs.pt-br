---
title: Comentários em HelloData | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925802"
---
# <a name="comments-on-hellodata"></a>Comentários sobre o HelloData
O aplicativo HelloData percorre as operações básicas de um aplicativo ADO típico: obtendo, examinando, editando e atualizando dados. Ao iniciar o aplicativo, clique no primeiro botão, **obtenha dados**. Isso executará a sub-rotina **GetData** .  
  
## <a name="getdata"></a>GetData  
 **GetData** coloca uma cadeia de conexão válida em uma variável em nível de módulo, *m_sConnStr*. Para obter mais informações sobre cadeias de conexão, consulte [criando a cadeia de conexão](../../../ado/guide/data/creating-a-connection-string.md).  
  
 Atribua um manipulador de erro usando uma instrução Visual Basic **OnError** . Para obter mais informações sobre o tratamento de erros no ADO, consulte [tratamento de erros](../../../ado/guide/data/error-handling.md). Um novo objeto de **conexão** é criado e a propriedade **CursorLocation** é definida como **adUseClient** porque o exemplo HelloData cria um *conjunto de registros desconectado*. Isso significa que assim que os dados são buscados da fonte de dados, a conexão física com a fonte de dados é interrompida, mas você ainda pode trabalhar com os dados armazenados em cache localmente no seu objeto **Recordset** .  
  
 Depois que a conexão for aberta, atribua uma cadeia de caracteres SQL a uma variável (sSQL). Em seguida, crie uma instância de **** um novo objeto `m_oRecordset1`recordset,. Na próxima linha de código, abra o **conjunto de registros** sobre a **conexão**existente, passando `sSQL` como a origem do **conjunto de registros**. Você ajuda o ADO em fazer a determinação de que a cadeia de caracteres SQL passada como a origem do **conjunto de registros** é uma definição textual de um comando, passando **adCmdText** no argumento final para o método Open do **conjunto de registros** . Essa linha também define o **LockType** e o **CursorType** associados ao **conjunto de registros**.  
  
 A próxima linha de código define a propriedade **marshaloptions** igual a **adMarshalModifiedOnly**. **Marshaloptions** indica quais registros devem ser empacotados para a camada intermediária (ou servidor Web). Para obter mais informações sobre marshaling, consulte a documentação COM. Quando você usa **adMarshalModifiedOnly** com um cursor do lado do cliente ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**), somente os registros que foram modificados no cliente são gravados novamente na camada intermediária. Definir **marshaloptions** para **adMarshalModifiedOnly** pode melhorar o desempenho porque menos linhas são empacotadas.  
  
 Em seguida, desconecte o **conjunto de registros** definindo sua propriedade **ActiveConnection** igual a **Nothing**. Para obter mais informações, consulte a seção "desconectando e reconectando o conjunto de registros" em [atualizando e mantendo dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Feche a conexão com a fonte de dados e destrua o objeto de **conexão** existente. Isso libera os recursos consumidos.  
  
 A etapa final é definir o **conjunto de registros** como a **fonte** de dados para o controle DataGrid da Microsoft no formulário, de modo que você possa exibir facilmente o dado do conjunto de **registros** no formulário.  
  
 Clique no segundo botão, **examine dados**. Isso executa a sub-rotina **ExamineData** .  
  
## <a name="examinedata"></a>ExamineData  
 O ExamineData usa vários métodos e propriedades do objeto **Recordset** para exibir informações sobre os dados no **conjunto de registros**. Ele relata o número de registros usando a propriedade **RecordCount** . Ele percorre o conjunto de **registros** e imprime o valor da propriedade **AbsolutePosition** na caixa de texto de exibição no formulário. Além disso, no loop, o valor da propriedade **Bookmark** para o terceiro registro é colocado em uma variável Variant, *vBookmark*, para uso posterior.  
  
 A rotina navega diretamente de volta para o terceiro registro usando a variável de indicador que ele armazenou anteriormente. A rotina chama a sub-rotina **WalkFields** , que percorre a coleção **Fields** do **conjunto de registros** e exibe detalhes sobre cada **campo** na coleção.  
  
 Por fim, **ExamineData** usa a propriedade **Filter** do **conjunto de registros** para fazer a tela apenas para os registros com uma **CategoryID** igual a 2. O resultado da aplicação desse filtro é imediatamente visível na grade de exibição no formulário.  
  
 Para obter mais informações sobre a funcionalidade mostrada na sub-rotina **ExamineData** , consulte [examinando dados](../../../ado/guide/data/examining-data.md).  
  
 Em seguida, clique no terceiro botão, **edite dados**. Isso executará a sub-rotina **EditData** .  
  
## <a name="editdata"></a>EditData  
 Quando o código entra na sub-rotina **EditData** , o **conjunto de registros** ainda é filtrado em **CategoryID** igual a 2, para que somente os itens que atendem aos critérios de filtro fiquem visíveis. Ele primeiro percorre o conjunto de **registros** e aumenta o preço de cada item visível no **conjunto de registros** em 10%. O valor do campo **preço** é alterado definindo a propriedade **valor** para esse campo igual a um valor novo e válido.  
  
 Lembre-se de que o **conjunto de registros** está desconectado da fonte de dados. As alterações feitas no **EditData** são feitas apenas para a cópia armazenada em cache localmente dos dados. Para obter mais informações, consulte [editando dados](../../../ado/guide/data/editing-data.md).  
  
 As alterações não serão feitas na fonte de dados até você clicar no quarto botão, **atualizar dados**. Isso executará a sub-rotina **UpdateData** .  
  
## <a name="updatedata"></a>UpdateData  
 O UpdateData primeiro remove o filtro que foi aplicado ao **conjunto de registros**. O código remove e redefine `m_oRecordset1` como a **fonte** de código para o DataGrid associado da Microsoft no formulário para que o **conjunto de registros** não filtrado seja exibido na grade.  
  
 Em seguida, o código verifica se você pode retroceder no **conjunto de registros** usando o método com **suporte** com o argumento **adMovePrevious** .  
  
 A rotina é movida para o primeiro registro usando o método **MoveFirst** e exibe os valores originais e atuais do campo, usando as propriedades **OriginalValue** e **valor** do objeto **Field** . Essas propriedades, juntamente com a propriedade **subdependent** (não usada aqui), são discutidas na [atualização e persistência de dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Em seguida, um novo objeto de **conexão** é criado e usado para restabelecer uma conexão com a fonte de dados. Reconecte o **conjunto de registros** à fonte de dados definindo a nova **conexão** como o **ActiveConnection** para o **conjunto de registros**. Para enviar as atualizações para o servidor, o código chama **UpdateBatch** no **conjunto de registros**.  
  
 Se a atualização do lote for realizada com sucesso, uma variável de sinalizador `m_flgPriceUpdated`de nível de módulo,, será definida como true. Isso o lembrará posteriormente de limpar todas as alterações feitas no banco de dados.  
  
 Por fim, o código volta para o primeiro registro no **conjunto de registros** e exibe os valores original e atual. Os valores são os mesmos após a chamada para **UpdateBatch**.  
  
 Para obter informações detalhadas sobre como atualizar dados, incluindo o que fazer quando os dados no servidor são alterados enquanto o **conjunto de registros** é desconectado, consulte [atualizando e mantendo dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
## <a name="form_unload"></a>Form_Unload  
 A sub-rotina **Form_Unload** é importante por vários motivos. Primeiro, como esse é um aplicativo de exemplo, Form_Unload limpa as alterações feitas no banco de dados antes do encerramento do aplicativo. Em segundo lugar, o código mostra como um comando pode ser executado diretamente de um objeto de **conexão** aberta usando o método **Execute** . Por fim, ele mostra um exemplo de execução de uma consulta de retorno que não é de linha (uma consulta de atualização) na fonte de dados.
