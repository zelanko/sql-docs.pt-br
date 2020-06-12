---
title: Conectar-se a um servidor de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
- getting started
ms.assetid: 85962ad6-d840-4bc6-905e-c667c3276944
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6e7fca367c72aaff5f02280829740942a36915ff
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527232"
---
# <a name="connect-to-a-data-mining-server"></a>Conectar a um servidor de mineração de dados
  ![Botão Conexões](media/misc-connection.gif "Botão Conexões")  
  
 Clique no botão **conexão** para selecionar uma conexão existente ou para criar uma nova conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 **Por que preciso me conectar a um servidor?**  
  
 Quando você cria uma conexão, isso lhe permite usar os algoritmos de mineração de dados fornecidos pelo servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e aproveitar o processamento otimizado do servidor.  
  
 Não é necessário manter os dados ou os resultados em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou do SQL Server. Os suplementos de mineração de dados do Excel só podem trabalhar com dados armazenados no Excel ou com dados aos quais você se conecta como uma origem de dados do Excel.  
  
## <a name="how-to-create-a-new-connection"></a>Como criar uma nova conexão  
  
1.  Clique no botão **conexão** .  
  
2.  Na caixa de diálogo **Analysis Services conexões** , clique em **novo**.  
  
3.  Na caixa de diálogo **conectar a Analysis Services** , digite um nome de servidor.  
  
4.  Especifique o método de autenticação.  
  
5.  Especifique o catálogo ou banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em que você armazenará os modelos de mineração de dados.  
  
    > [!NOTE]  
    >  Caso ainda não tenha criado bancos de dados, você poderá usar (padrão) para criar e depois testar a conexão; no entanto, não é possível adicionar modelos de mineração à conexão padrão. Antes de criar modelos de mineração, você deve criar uma conexão com um banco de dados existente.  
  
6.  Se você estiver se conectando ao servidor por meio de um serviço Web, digite o nome de usuário e a senha necessários para esse serviço Web.  
  
7.  Digite um nome amigável para a nova conexão.  
  
8.  Clique em **testar conexão** para verificar se o servidor está disponível.  
  
## <a name="troubleshooting-connections"></a>Solucionando problemas de conexões  
 Esta seção fornece respostas para algumas das perguntas mais comuns sobre conexões ao [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Recebo uma mensagem dizendo "nenhuma conexão encontrada".**  
  
 Se o texto na parte inferior do botão **não diz nenhuma conexão**, isso significa que você não criou uma conexão com um banco de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] dados ou que a conexão falhou. Você pode continuar trabalhando com os dados no Excel pelo Access ou outras origens, mas para criar um modelo de mineração de dados ou executar uma consulta de previsão, é necessário ter uma conexão ativa.  
  
 **Suponha que eu não tenha permissão para usar o servidor?**  
  
 Se você não tiver permissões suficientes para armazenar os modelos de mineração no servidor, ou se quiser fazer experiências com a mineração de dados sem salvar o trabalho, poderá usar as Ferramentas de Análise de Tabela, que criam estruturas de dados temporárias e modelos temporários. Você ainda precisa ser capaz de armazenar modelos temporários no servidor. Peça ao administrador para habilitar o uso de *modelos de mineração de sessão* no servidor.  
  
 Se você quiser garantir que os modelos sejam salvos, poderá desabilitar a opção para usar modelos temporários, ou usar os assistentes no Cliente de Mineração de Dados. Esses assistentes armazenam todos os modelos no servidor. Você precisará ter acesso administrativo ao banco de dados onde os modelos são armazenados; então, é recomendável solicitar ao administrador que crie um banco de dados especialmente para a criação de modelos de mineração com os suplementos.  
  
 **Perdi minha conexão; perdi todo o meu trabalho?**  
  
 Se você encerrar a conexão ao servidor, seus resultados e seus dados não serão perdidos, uma vez que estão armazenados no Excel. Entretanto, se você tiver criado modelos temporários, esses modelos serão excluídos do servidor após um período curto. Portanto, se você perder a conexão temporariamente, alguns modelos ainda não serão excluídos.  
  
 Dados ou resultados que tenham sido gerados não serão perdidos, pois todos os relatórios e tabelas são armazenados no Excel.  
  
> [!NOTE]  
>  Não se desconecte do servidor ou da rede enquanto o suplemento estiver se comunicando com o servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Por exemplo, nunca desconecte quando um modelo estiver sendo criado ou quando os dados estiverem sendo processados. Em algumas situações, os dados poderão ser corrompidos.  
  
 **Não consigo me conectar ao modelo usando as ferramentas do Visio**  
  
 Os Modelos de Mineração de Dados para Visio não podem utilizar estruturas e modelos de mineração temporários. Para criar um diagrama de um modelo de mineração, o modelo deve ser armazenado em um servidor.  
  
 **Como posso monitorar o uso da conexão?**  
  
 A ferramenta [rastrear &#40;cliente de mineração de dados para Excel&#41;](trace-data-mining-client-for-excel.md) cria um log de todas as atividades entre os suplementos e o servidor especificado.  
  
 Para habilitar o monitoramento de modelos de sessão, selecione a opção **usar modelos de sessão** na caixa de diálogo **rastreador** .  
  
 O rastreamento permite que você exiba os comandos DMX e XMLA gerados durante a criação de modelos e estruturas. Também é possível exibir as consultas enviadas pelo cliente para gerar resultados e relatórios no Excel.  
  
 **O que é um modelo temporário? Como posso salvar um modelo temporário?**  
  
 As Ferramentas de Análise de Tabela para Excel por padrão criam estruturas de dados e modelos de mineração temporários. Você pode continuar navegando e consultando modelos temporários, contanto que mantenha a pasta de trabalho aberta e não se desconecte do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 As estruturas e modelos de sessão criados serão excluídos assim que você fechar a pasta de trabalho do Excel ou caso você altere ou encerre sua conexão com o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Quando você concluir um assistente no Cliente de Mineração de Dados para Excel, modelos serão salvos no servidor por padrão, mas na página final de cada assistente existe a opção de usar um modelo temporário. Se você selecionar essa opção, a estrutura e o modelo de mineração de dados que criar serão armazenados em um arquivo temporário. Você poderá procurar, gerenciar e modificar a estrutura e o modelo, desde que o Excel permaneça aberto. Porém, depois que você fechar o Excel, a estrutura e os modelos relacionados serão excluídos.  
  
 Você também pode criar explicitamente uma estrutura ou modelo temporário usando o **Editor de consulta avançada de mineração de dados** e selecionando um dos modelos DMX. Adicione a cláusula `USE SESSION MODELS` para especificar que os objetos sejam temporários.   
  
### <a name="creating-backups-of-mining-models-and-structures"></a>Criando backups de modelos e estruturas de mineração  
 Para criar um backup de um modelo ou estrutura, você pode exportá-lo usando [gerenciar modelos &#40;SQL Server suplementos de mineração de dados&#41;](manage-models-sql-server-data-mining-add-ins.md), no cliente de mineração de dados para Excel.  
  
 Se você criou um modelo de mineração temporário, tipicamente ele terá um nome difícil de compreender, como Table5_593679_TS_62446. No entanto, você pode usar a ferramenta [rastrear &#40;cliente de mineração de dados para Excel&#41;](trace-data-mining-client-for-excel.md) para descobrir os nomes de estruturas temporárias e modelos que foram criados pelas ferramentas de análise de tabela e, em seguida, fazer backup deles usando **gerenciar modelos**.  
  
##### <a name="identify-and-export-a-temporary-model"></a>Identifique e exporte um modelo temporário  
  
1.  No grupo **conexões** do cliente de mineração de dados para Excel, clique em **rastrear**.  
  
2.  Exibir o log de atividades de conexão e localize o modelo ao examinar as colunas e os resultados previsíveis (por exemplo).  
  
     Usuários avançados: se você tiver experiência com DMX ou XMLA, poderá copiar as instruções para um arquivo para uso posterior.  
  
3.  Quando você encontrar o nome do modelo temporário e a estrutura, abra **gerenciar modelo** e selecione o modelo.  
  
4.  Clique em Exportar este modelo de mineração para gerar um arquivo de script em um local especificado por você.  
  
## <a name="see-also"></a>Consulte Também  
 [Conectar-se a dados de origem &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md)   
 [Utilitário de configuração do servidor &#40;suplementos de mineração de dados para Excel&#41;](server-configuration-utility-data-mining-add-ins-for-excel.md)  
  
  
