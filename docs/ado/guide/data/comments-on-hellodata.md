---
title: Comentários sobre HelloData | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5156c6faacb9714faa40073d2a0f78102663b4b0
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271435"
---
# <a name="comments-on-hellodata"></a>Comentários sobre HelloData
O aplicativo HelloData percorre as operações básicas de um aplicativo típico do ADO: obtendo, examinando, editar e atualizar dados. Quando você inicia o aplicativo, clique no primeiro botão, **obter dados**. Isso executará o **GetData** sub-rotina.  
  
## <a name="getdata"></a>GetData  
 **GetData** coloca uma cadeia de caracteres de conexão válido em uma variável de nível de módulo, *m_sConnStr*. Para obter mais informações sobre cadeias de caracteres de conexão, consulte [criar a cadeia de caracteres de Conexão](../../../ado/guide/data/creating-a-connection-string.md).  
  
 Atribuir um manipulador de erro usando um Visual Basic **OnError** instrução. Para obter mais informações sobre tratamento de erros no ADO, consulte [tratamento de erros](../../../ado/guide/data/error-handling.md). Um novo **Conexão** objeto é criado e o **CursorLocation** está definida como **adUseClient** porque o exemplo HelloData cria um  *Recordset desconectado*. Isso significa que, assim como os dados tiverem sido buscados da fonte de dados, a conexão física com a fonte de dados é interrompida, mas você ainda pode trabalhar com os dados armazenados em cache localmente no seu **registros** objeto.  
  
 Depois que a conexão tiver sido aberto, atribua uma cadeia de caracteres SQL para uma variável (sSQL). Em seguida, crie uma instância de um novo **registros** objeto `m_oRecordset1`. Na próxima linha de código, abra o **registros** sobre existente **Conexão**, passando `sSQL` como a fonte do **registros**. Ajudar o ADO para fazer a determinação do que o SQL da cadeia de caracteres é ter passado como a origem para o **Recordset** é uma definição textual de um comando, passando **adCmdText** no argumento final para o **Abrir conjunto de registros** método. Esta linha também define o **LockType** e **CursorType** associados a **registros**.  
  
 A próxima linha do código define o **MarshalOptions** propriedade igual a **adMarshalModifiedOnly**. **MarshalOptions** indica quais registros devem ser empacotados para a camada intermediária (ou o servidor Web). Para obter mais informações sobre o empacotamento, consulte a documentação de COM. Quando você usa **adMarshalModifiedOnly** com um cursor do lado do cliente ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**), somente os registros que tiverem sido modificados a cliente são gravados de volta para a camada intermediária. Configuração **MarshalOptions** para **adMarshalModifiedOnly** pode melhorar o desempenho porque menos linhas são empacotadas.  
  
 Em seguida, desconecte o **registros** definindo seu **ActiveConnection** propriedade igual a **nada**. Para obter mais informações, consulte a seção "Desconectar e reconectar-se o conjunto de registros" em [atualizando e persistir dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Feche a conexão à fonte de dados e destruir existente **Conexão** objeto. Isso libera os recursos consumidos por ele.  
  
 A etapa final é definir o **Recordset** como o **fonte de dados** para a grade de dados do Microsoft controle no formulário assim que você pode exibir facilmente os dados do **Recordset** no formulário.  
  
 Clique no botão segundo **examinar dados**. Isso executará o **ExamineData** sub-rotina.  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData usa vários métodos e propriedades do **Recordset** objeto para exibir informações sobre os dados a **Recordset**. Informa o número de registros usando o **RecordCount** propriedade. Percorre o **registros** e imprime o valor do **AbsolutePosition** propriedade na caixa de texto de exibição no formulário. Também enquanto estiver no loop, o valor da **indicador** propriedade para o terceiro registro é colocada em uma variável variant, *vBookmark*, para uso posterior.  
  
 A rotina diretamente navega de volta para o terceiro registro usando a variável de indicador armazenado anteriormente. As chamadas de rotina de **WalkFields** sub-rotina, que percorre o **campos** coleção do **Recordset** e exibe os detalhes sobre cada **campo**  na coleção.  
  
 Por fim, **ExamineData** usa o **filtro** propriedade o **Recordset** tela somente os registros com um **CategoryId** igual a 2. O resultado da aplicação desse filtro fica imediatamente visível na grade de exibição no formulário.  
  
 Para obter mais informações sobre a funcionalidade que mostra o **ExamineData** sub-rotina, consulte [examinando dados](../../../ado/guide/data/examining-data.md).  
  
 Em seguida, clique no botão de terceiro, **editar dados**. Isso executará o **EditData** sub-rotina.  
  
## <a name="editdata"></a>EditData  
 Quando o código entra o **EditData** sub-rotina, o **registros** ainda é filtrado em **CategoryId** igual a 2, para que somente os itens que atendem aos critérios de filtro visível. Primeiro percorre o **registros** e aumenta o preço de cada item visível no **registros** 10 por cento. O valor da **preço** campo é alterado, definindo o **valor** propriedade desse campo igual a um valor novo, válido.  
  
 Lembre-se de que o **registros** está desconectado da fonte de dados. As alterações feitas no **EditData** são feitas apenas para a cópia localmente em cache dos dados. Para obter mais informações, consulte [edição dados](../../../ado/guide/data/editing-data.md).  
  
 As alterações não serão feitas na fonte de dados até que você clique no botão quarto **atualização dados**. Isso executará o **UpdateData** sub-rotina.  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData primeiro remove o filtro que foi aplicado para o **registros**. O código remove e redefine `m_oRecordset1` como o **a fonte de dados** para DataGrid Microsoft associado no formulário para que o não filtrado **Recordset** aparece na grade.  
  
 O código, em seguida, verifica se você pode retroceder **registros** usando o **dá suporte a** método com o **adMovePrevious** argumento.  
  
 A rotina move para o primeiro registro usando o **MoveFirst** método e exibe os valores do campo original e atual, usando o **OriginalValue** e **valor** Propriedades do **campo** objeto. Essas propriedades, juntas com o **UnderlyingValue** propriedade (não usado aqui), são discutidos em [atualizando e persistir dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Em seguida, um novo **Conexão** objeto é criado e usado para restabelecer uma conexão à fonte de dados. Reconectar o **registros** à fonte de dados, definindo o novo **Conexão** como o **ActiveConnection** para o **registros**. Para enviar as atualizações para o servidor, o código chama **UpdateBatch** no **registros**.  
  
 Se a atualização em lotes tiver êxito, uma variável de sinalizador de nível de módulo, `m_flgPriceUpdated`, está definido como True. Isso irá lembrá-lo posteriormente para limpar todas as alterações feitas no banco de dados.  
  
 Por fim, o código de volta para o primeiro registro de **registros** e exibe os valores atuais e originais. Os valores são as mesmas após a chamada a **UpdateBatch**.  
  
 Para obter informações detalhadas sobre como atualizar dados, incluindo o que fazer quando dados sobre as alterações de servidor ao seu **registros** é desconectado, consulte [atualizando e persistir dados](../../../ado/guide/data/updating-and-persisting-data.md).  
  
## <a name="formunload"></a>Form_Unload  
 O **Form_Unload** sub-rotina é importante por vários motivos. Primeiro, porque este é um aplicativo de exemplo, Form_Unload limpa as alterações feitas no banco de dados antes de sair do aplicativo. Segundo, o código mostra como um comando pode ser executado diretamente de um aberto **Conexão** objeto usando o **Execute** método. Finalmente, ele mostra um exemplo de execução de uma consulta não retornar ao linha (uma consulta UPDATE) em relação à fonte de dados.
