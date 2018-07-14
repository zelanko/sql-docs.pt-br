---
title: Configurar a transformação de comando OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- parameters [Integration Services]
- OLE DB Command transformation
ms.assetid: c800f167-3d2e-4c10-8ba3-a02f1872ccea
caps.latest.revision: 24
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a29642a667d4d22ecf5c7f6d3de0848b4725df91
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254478"
---
# <a name="configure-the-ole-db-command-transformation"></a>Configurar a transformação Comando OLE DB
  Para adicionar e configurar uma transformação Comando OLE DB, o pacote já deve incluir pelo menos uma tarefa Fluxo de Dados e uma origem, como, por exemplo, uma origem de arquivo simples ou uma origem de OLE DB. Essa transformação é normalmente usada para executar consultas parametrizadas.  
  
### <a name="to-configure-the-ole-db-command-transformation"></a>Para configurar a transformação Comando OLE DB  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste a transformação Comando OLE DB para a superfície de design.  
  
4.  Conecte a transformação Comando OLE DB ao fluxo de dados, arrastando um conector – a seta verde ou vermelha – de uma origem de dados ou uma transformação anterior para a transformação Comando OLE DB.  
  
5.  Com o botão direito do mouse, clique no componente e selecione Editar ou Mostrar **Editor Avançado**.  
  
6.  Na guia **Gerenciadores de Conexões** , selecione um gerenciador de conexões OLE DB na lista **Gerenciador de Conexões** . Para obter mais informações, consulte [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md).  
  
7.  Clique na guia **Propriedades do Componente** e clique no botão de reticências **(...)** , na caixa **SqlCommand** .  
  
8.  No **Editor de Valores de Cadeias de Caracteres**, digite a instrução SQL parametrizada, com o uso de um ponto de interrogação (?) como o marcador para cada parâmetro.  
  
9. Clique em **Atualizar**. Quando você clica em **Atualizar**, a transformação cria uma coluna para cada parâmetro na coleção Colunas Externas e define a propriedade DBParamInfoFlags.  
  
10. Clique na guia **Propriedades de Entrada e Saída** .  
  
11. Expanda **Entrada de Comando OLE DB**e **Colunas Externas**.  
  
12. Verifique se **Colunas Externas** lista uma coluna para cada parâmetro na instrução SQL. Os nomes das colunas são **Param_0**, **Param_1**e assim por diante.  
  
     Você não deve alterar os nomes de coluna. Se você alterar os nomes de coluna, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] gerará um erro de validação para a transformação Comando OLE DB.  
  
     Além disso, você não dever alterar o tipo de dados. A propriedade DataType de cada coluna é definida como o tipo de dados correto.  
  
13. Se **Colunas Externas** não listar nenhuma coluna, você terá que adicioná-las manualmente.  
  
    -   Clique em **Adicionar Coluna** uma vez para cada parâmetro na instrução SQL.  
  
    -   Atualize os nomes das colunas para **Param_0**, **Param_1**, e assim por diante.  
  
    -   Especifique um valor na propriedade DBParamInfoFlags. O valor deve corresponder a um valor da enumeração OLE DB DBPARAMFLAGSENUM. Para obter mais informações, consulte a documentação de referência do OLE DB.  
  
    -   Especifique o tipo de dados da coluna e, dependendo do tipo de dados, especifique a página de código, o comprimento, a precisão e a escala da coluna.  
  
    -   Para excluir um parâmetro não utilizado, selecione o parâmetro em **Colunas Externas**e clique em **Remover Coluna**.  
  
    -   Clique em **Mapeamentos de Colunas** e mapeie colunas da lista **Colunas de Entrada Disponíveis** para parâmetros na lista **Colunas de Destino Disponíveis** .  
  
14. Clique em **OK**.  
  
15. Para salvar o pacote atualizado, clique em **Salvar** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte também  
 [Transformação comando OLE DB](data-flow/transformations/ole-db-command-transformation.md)   
 [Transformações do Integration Services](data-flow/transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](data-flow/integration-services-paths.md)   
 [Tarefa de Fluxo de Dados](control-flow/data-flow-task.md)  
  
  
