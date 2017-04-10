---
title: "Mapear par&#226;metros de consulta para vari&#225;veis em um componente de fluxo de dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "consultas [Integration Services], mapeamento de parâmetro"
  - "parâmetros [Integration Services]"
  - "mapeando parâmetros de consulta para variáveis [Integration Services]"
  - "variáveis [Integration Services], mapeando parâmetros para"
ms.assetid: 5e26977c-758c-46d6-acf1-4fd9238f0950
caps.latest.revision: 34
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 34
---
# Mapear par&#226;metros de consulta para vari&#225;veis em um componente de fluxo de dados
  Quando você configura a fonte OLE DB para usar consultas parametrizadas, pode mapear os parâmetros para variáveis.  
  
 As fontes OLE DB usam consultas parametrizadas para filtrar dados quando a fonte conecta-se a uma fonte de dados.  
  
### Para mapear um parâmetro de consulta para uma variável  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste a fonte OLE DB para a superfície de design.  
  
4.  Clique com o botão direito do mouse na fonte OLE DB e, depois, clique em **Editar**.  
  
5.  Em **Editor de Origem OLE DB**, selecione um gerenciador de conexões para usar para conectar-se à fonte de dados ou clique em **Novo** para criar um novo gerenciador de conexões OLE DB.  
  
6.  Selecione a opção de **Comando SQL** para o modo de acesso a dados e, então, digite uma consulta parametrizada no painel **Texto de comando SQL**.  
  
7.  Clique em **Parâmetros**.  
  
8.  Na caixa de diálogo **Definir Parâmetros de Consulta**, mapeie cada parâmetro na lista **Parâmetros** a uma variável na lista **Variáveis** ou crie uma nova variável clicando em **\<Nova variável>**. Clique em **OK**.  
  
    > [!NOTE]  
    >  Apenas as variáveis do sistema e as variáveis definidas pelo usuário que estão no escopo do pacote, um contêiner pai como Loop Foreach ou a tarefa de Fluxo de Dados que contém o componente de fluxo de dados, estão disponíveis para mapeamento. A variável deve ter um tipo de dados que seja compatível com a coluna na cláusula WHERE, para a qual o parâmetro é designado.  
  
9. Você pode clicar em **Visualizar** para exibir até 200 linhas dos dados que a consulta retorna.  
  
10. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## Consulte também  
 [Origem de OLE DB](../../integration-services/data-flow/ole-db-source.md)   
 [Transformação Pesquisa](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  