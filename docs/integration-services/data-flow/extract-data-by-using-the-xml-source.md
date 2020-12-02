---
description: Extrair dados por meio da origem XML
title: Extrair dados usando a origem XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], XML
- XML source [Integration Services]
ms.assetid: 5d5be54c-2b7e-4957-9193-c5ea5c5d6d15
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f3cd306d2cf6097fdb5e178f92e41d45de198783
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127169"
---
# <a name="extract-data-by-using-the-xml-source"></a>Extrair dados por meio da origem XML

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
  
9. Para configurar a saída de erro, clique em **Saída de Erro**. Para obter mais informações, consulte [Debugging Data Flow](../../integration-services/troubleshooting/debugging-data-flow.md).  
  
10. Clique em **OK**.  
  
11. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Origem XML](../../integration-services/data-flow/xml-source.md)   
 [Transformações do Integration Services](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](../../integration-services/data-flow/integration-services-paths.md)   
 [Tarefa de Fluxo de Dados](../../integration-services/control-flow/data-flow-task.md)  
  
  
