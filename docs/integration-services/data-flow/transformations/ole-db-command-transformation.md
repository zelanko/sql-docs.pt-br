---
title: Transformação Comando OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbcommandtrans.f1
helpviewer_keywords:
- statements [Integration Services]
- OLE DB Command transformation
ms.assetid: baa6735c-5acf-4759-b077-1216aca16c6c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 09850707b83481909a881dcefdf00e710e6a8790
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71291242"
---
# <a name="ole-db-command-transformation"></a>transformação Comando OLE DB

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A transformação Comando OLE DB executa uma instrução SQL para cada linha do fluxo de dados. Por exemplo, você pode executar uma instrução SQL que insira, atualize ou exclua linhas em uma tabela de banco de dados.  
  
 É possível configurar a transformação Comando OLE DB com os seguintes procedimentos:  
  
-   Forneça a instrução SQL que a transformação executa para cada linha.  
  
-   Especifique o número de segundos antes que a instrução SQL expire.  
  
-   Especifique a página de código padrão.  
  
 Normalmente, a instrução SQL inclui parâmetros. Os valores de parâmetro são armazenados em colunas externas na entrada da transformação e o mapeamento de uma coluna de entrada para uma coluna externa mapeia uma coluna de entrada para um parâmetro. Por exemplo, para localizar linhas na tabela **DimProduct** pelo valor da coluna **ProductKey** e, em seguida, excluí-las, você pode mapear a coluna externa nomeada como **Param_0** para a coluna de entrada nomeada como **ProductKey** e, em seguida, executar a instrução SQL `DELETE FROM DimProduct WHERE ProductKey = ?`. A transformação Comando OLE DB fornece os nomes de parâmetro e você não pode modificá-los. Os nomes de parâmetro são **Param_0**, **Param_1**e assim por diante.  
  
 Se você configurar a transformação Comando OLE DB usando a caixa de diálogo **Editor Avançado** , os parâmetros na instrução SQL poderão ser mapeados automaticamente para colunas externas na entrada da transformação e as características de cada parâmetro poderão ser definidas, clicando no botão **Atualizar** . Entretanto, se o provedor OLE DB que a transformação Comando OLE DB usa não oferecer suporte para derivação de informações do parâmetro, você deverá configurar as colunas externas manualmente. Isto significa que você deve adicionar uma coluna para cada parâmetro na entrada externa para a transformação, atualizar os nomes de coluna para usar nomes como **Param_0**, especificar o valor da propriedade DBParamInfoFlags e mapear as colunas de entrada que contêm valores de parâmetro para as colunas externas.  
  
 O valor da propriedade DBParamInfoFlags representa as características do parâmetro. Por exemplo, o valor **1** especifica que o parâmetro é de entrada e o valor **65** especifica que o parâmetro é de entrada e pode conter um valor nulo. Os valores devem corresponder aos da enumeração OLE DB DBPARAMFLAGSENUM. Para obter mais informações, consulte a documentação de referência do OLE DB.  
  
 A transformação Comando OLE DB inclui a propriedade personalizada **SQLCommand** . Essa propriedade pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Essa transformação tem uma entrada, uma saída comum e uma saída de erro.  
  
## <a name="logging"></a>Log  
 Você poderá fazer log das chamadas que a transformação Comando OLE DB fizer a provedores de dados externos. Você pode usar esse recurso de log para solucionar problemas de conexões e comandos das fontes de dados externos executados pela transformação Comando OLE DB. Para fazer log das chamadas que a transformação Comando OLE DB fizer aos provedores de dados externos, habilite o log do pacote e selecione o evento **Diagnóstico** no nível de pacote. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 Você pode configurar a transformação por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer ou do modelo de objeto. Consulte o Guia do Desenvolvedor para obter detalhes sobre como configurar essa transformação programaticamente.  
  
## <a name="configure-the-ole-db-command-transformation"></a>Configurar a transformação Comando OLE DB
  Para adicionar e configurar uma transformação Comando OLE DB, o pacote já deve incluir pelo menos uma tarefa Fluxo de Dados e uma origem, como, por exemplo, uma origem de arquivo simples ou uma origem de OLE DB. Essa transformação é normalmente usada para executar consultas parametrizadas.  
  
#### <a name="to-configure-the-ole-db-command-transformation"></a>Para configurar a transformação Comando OLE DB  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** e, na **Caixa de Ferramentas**, arraste a transformação Comando OLE DB para a superfície de design.  
  
4.  Conecte a transformação Comando OLE DB ao fluxo de dados arrastando um conector (a seta verde ou vermelha) de uma fonte de dados ou de uma transformação anterior para a transformação Comando OLE DB.  
  
5.  Com o botão direito do mouse, clique no componente e selecione Editar ou Mostrar **Editor Avançado**.  
  
6.  Na guia **Gerenciadores de Conexões** , selecione um gerenciador de conexões OLE DB na lista **Gerenciador de Conexões** . Para obter mais informações, consulte [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
7.  Clique na guia **Propriedades do Componente** e clique no botão de reticências **(...)** na caixa **SqlCommand**.  
  
8.  No **Editor de Valores de Cadeias de Caracteres**, digite a instrução SQL parametrizada, com o uso de um ponto de interrogação (?) como o marcador para cada parâmetro.  
  
9. Clique em **Atualizar**. Quando você clica em **Atualizar**, a transformação cria uma coluna para cada parâmetro na coleção Colunas Externas e define a propriedade DBParamInfoFlags.  
  
10. Clique na guia **Propriedades de Entrada e Saída** .  
  
11. Expanda **Entrada de Comando OLE DB**e **Colunas Externas**.  
  
12. Verifique se **Colunas Externas** lista uma coluna para cada parâmetro na instrução SQL. Os nomes das colunas são **Param_0**, **Param_1**e assim por diante.  
  
     Você não deve alterar os nomes de coluna. Se você alterar os nomes de coluna, o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] gerará um erro de validação para a transformação Comando OLE DB.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
