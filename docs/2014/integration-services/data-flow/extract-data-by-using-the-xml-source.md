---
title: Extrair dados usando a origem XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], XML
- XML source [Integration Services]
ms.assetid: 5d5be54c-2b7e-4957-9193-c5ea5c5d6d15
author: janinezhang
ms.author: janinez
ms.openlocfilehash: fcf27faf2678aa89c0fa646c0a1b3f7b4d9401c3
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915656"
---
# <a name="extract-data-by-using-the-xml-source"></a>Extrair dados por meio da origem XML
  Para adicionar e configurar uma origem XML, o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados.  
  
### <a name="to-extract-data-using-an-xml-source"></a>Para extrair dados usando uma origem XML  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste a origem XML para a superfície de design.  
  
4.  Clique duas vezes na origem XML.  
  
5.  No **Editor de Origem XML**, na página **Gerenciador de Conexões** , selecione um modo de acesso a dados:  
  
    -   Para o modo de acesso **Local de arquivo XML** , clique em **Procurar** e localize a pasta que contém o arquivo XML.  
  
    -   Para o modo de acesso **Arquivo XML de variável** , selecione a variável definida pelo usuário que contém o caminho do arquivo XML.  
  
    -   Para o modo de acesso **Dados XML de variável** , selecione a variável definida pelo usuário que contém os dados XML.  
  
    > [!NOTE]  
    >  As variáveis devem ser definidas no escopo da tarefa Fluxo de Dados que contém a origem XML ou no escopo do pacote, além disso, a variável deve ter um tipo de dados de cadeia de caracteres.  
  
6.  Como opção, selecione **Usar esquema embutido** para indicar se o documento XML inclui informações de esquema.  
  
7.  Para especificar um esquema XSD (linguagem de definição de esquema XML) externo para o arquivo XML, execute uma das seguintes ações:  
  
    -   Clique em **Procurar** para localizar um arquivo XSD existente.  
  
    -   Clique em **Gerar XSD** para criar um XSD por meio do arquivo XML.  
  
8.  Para atualizar os nomes das colunas de saída, clique em **Colunas** e edite os valores na lista **Coluna de Saída** .  
  
9. Para configurar a saída de erro, clique em **Saída de Erro**. Para obter mais informações, consulte [Configurar uma saída de erro em um componente de fluxo de dados](../configure-an-error-output-in-a-data-flow-component.md).  
  
10. Clique em **OK**.  
  
11. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Origem XML](xml-source.md)   
 [Transformações do Integration Services](transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](integration-services-paths.md)   
 [Tarefa de Fluxo de Dados](../control-flow/data-flow-task.md)  
  
  
