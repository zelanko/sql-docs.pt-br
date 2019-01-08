---
title: Conectar a um servidor de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
- getting started
ms.assetid: 85962ad6-d840-4bc6-905e-c667c3276944
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9ca50a030fef65c9de02bc93dcd970df2686b0a
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52420387"
---
# <a name="connect-to-a-data-mining-server"></a>Conectar a um servidor de mineração de dados
  ![Botão de conexões](media/misc-connection.gif "botão conexões")  
  
 Clique o **Conexão** botão para selecionar uma conexão existente ou criar uma nova conexão a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Por que precisa para se conectar a um servidor?**  
  
 Quando você cria uma conexão, isso lhe permite usar os algoritmos de mineração de dados fornecidos pelo servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e aproveitar o processamento otimizado do servidor.  
  
 Não é necessário manter os dados ou os resultados em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou do SQL Server. Os suplementos de mineração de dados do Excel só podem trabalhar com dados armazenados no Excel ou com dados aos quais você se conecta como uma origem de dados do Excel.  
  
## <a name="how-to-create-a-new-connection"></a>Como criar uma nova conexão  
  
1.  Clique o **Conexão** botão.  
  
2.  No **conexões do Analysis Services** caixa de diálogo, clique em **New**.  
  
3.  No **conectar ao Analysis Services** caixa de diálogo, digite um nome de servidor.  
  
4.  Especifique o método de autenticação.  
  
5.  Especifique o catálogo ou banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em que você armazenará os modelos de mineração de dados.  
  
    > [!NOTE]  
    >  Caso ainda não tenha criado bancos de dados, você poderá usar (padrão) para criar e depois testar a conexão; no entanto, não é possível adicionar modelos de mineração à conexão padrão. Antes de criar modelos de mineração, você deve criar uma conexão com um banco de dados existente.  
  
6.  Se você estiver se conectando ao servidor por meio de um serviço Web, digite o nome de usuário e a senha necessários para esse serviço Web.  
  
7.  Digite um nome amigável para a nova conexão.  
  
8.  Clique em **Conexão de teste** para verificar se o servidor está disponível.  
  
## <a name="troubleshooting-connections"></a>Solucionando problemas de conexões  
 Esta seção fornece respostas para algumas das perguntas mais comuns sobre conexões ao [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Recebo uma mensagem não dizendo "Nenhuma conexão encontrada".**  
  
 Se o texto na parte inferior do botão diz **nenhuma Conexão**, isso significa que você não tiver criado uma conexão para um [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados ou que a conexão falhou. Você pode continuar trabalhando com os dados no Excel pelo Access ou outras origens, mas para criar um modelo de mineração de dados ou executar uma consulta de previsão, é necessário ter uma conexão ativa.  
  
 **Suponha que eu não tenho permissão para usar o servidor?**  
  
 Se você não tiver permissões suficientes para armazenar os modelos de mineração no servidor, ou se quiser fazer experiências com a mineração de dados sem salvar o trabalho, poderá usar as Ferramentas de Análise de Tabela, que criam estruturas de dados temporárias e modelos temporários. Você ainda precisa ser capaz de armazenar modelos temporários no servidor. Solicite ao administrador para habilitar o uso de *modelos de mineração de sessão* no servidor.  
  
 Se você quiser garantir que os modelos sejam salvos, poderá desabilitar a opção para usar modelos temporários, ou usar os assistentes no Cliente de Mineração de Dados. Esses assistentes armazenam todos os modelos no servidor. Você precisará ter acesso administrativo ao banco de dados onde os modelos são armazenados; então, é recomendável solicitar ao administrador que crie um banco de dados especialmente para a criação de modelos de mineração com os suplementos.  
  
 **Perdi minha conexão; Perdi todo o meu trabalho?**  
  
 Se você encerrar a conexão ao servidor, seus resultados e seus dados não serão perdidos, uma vez que estão armazenados no Excel. Entretanto, se você tiver criado modelos temporários, esses modelos serão excluídos do servidor após um período curto. Portanto, se você perder a conexão temporariamente, em algum momento os modelos não terão sido excluídos.  
  
 Dados ou resultados que tenham sido gerados não serão perdidos, pois todos os relatórios e tabelas são armazenados no Excel.  
  
> [!NOTE]  
>  Não se desconecte do servidor ou da rede enquanto o suplemento estiver se comunicando com o servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Por exemplo, nunca desconecte quando um modelo estiver sendo criado ou quando os dados estiverem sendo processados. Em algumas situações, os dados poderão ser corrompidos.  
  
 **Não é possível conectar-se ao modelo usando as ferramentas do Visio**  
  
 Os Modelos de Mineração de Dados para Visio não podem utilizar estruturas e modelos de mineração temporários. Para criar um diagrama de um modelo de mineração, o modelo deve ser armazenado em um servidor.  
  
 **Como monitorar o uso da conexão?**  
  
 O [rastreamento &#40;cliente de mineração de dados para Excel&#41; ](trace-data-mining-client-for-excel.md) ferramenta cria um log de todas as atividades entre os suplementos e o servidor especificado.  
  
 Para habilitar o monitoramento de modelos de sessão, selecione a **usar modelos de sessão** opção a **rastreamento** caixa de diálogo.  
  
 O rastreamento permite que você exiba os comandos DMX e XMLA gerados durante a criação de modelos e estruturas. Também é possível exibir as consultas enviadas pelo cliente para gerar resultados e relatórios no Excel.  
  
 **O que é um modelo temporário? Como salvar um modelo temporário?**  
  
 As Ferramentas de Análise de Tabela para Excel por padrão criam estruturas de dados e modelos de mineração temporários. Você pode continuar navegando e consultando modelos temporários, contanto que mantenha a pasta de trabalho aberta e não se desconecte do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 As estruturas e modelos de sessão criados serão excluídos assim que você fechar a pasta de trabalho do Excel ou caso você altere ou encerre sua conexão com o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Quando você concluir um assistente no Cliente de Mineração de Dados para Excel, modelos serão salvos no servidor por padrão, mas na página final de cada assistente existe a opção de usar um modelo temporário. Se você selecionar essa opção, a estrutura e o modelo de mineração de dados que criar serão armazenados em um arquivo temporário. Você poderá procurar, gerenciar e modificar a estrutura e o modelo, desde que o Excel permaneça aberto. Porém, depois que você fechar o Excel, a estrutura e os modelos relacionados serão excluídos.  
  
 Você pode também criar explicitamente uma estrutura ou modelo temporário usando o **dados Editor avançada de mineração consulta** e selecionando um dos modelos DMX. Adicione a cláusula `USE SESSION MODELS` para especificar que os objetos sejam temporários.   
  
### <a name="creating-backups-of-mining-models-and-structures"></a>Criando backups de modelos e estruturas de mineração  
 Para criar um backup de um modelo ou estrutura, você pode exportá-lo usando [gerenciar modelos &#40;SQL Server Data Mining Add-ins&#41;](manage-models-sql-server-data-mining-add-ins.md), no cliente de mineração de dados para Excel.  
  
 Se você criou um modelo de mineração temporário, tipicamente ele terá um nome difícil de compreender, como Table5_593679_TS_62446. No entanto, você pode usar o [rastreamento &#40;cliente de mineração de dados para Excel&#41; ](trace-data-mining-client-for-excel.md) ferramenta para descobrir os nomes das estruturas temporárias e modelos que foram criados pelas ferramentas de análise de tabela e, em seguida, fazer backup deles usando  **Gerenciar modelos**.  
  
##### <a name="identify-and-export-a-temporary-model"></a>Identifique e exporte um modelo temporário  
  
1.  No **conexões** grupo do cliente de mineração de dados para Excel, clique em **rastreamento**.  
  
2.  Exibir o log de atividades de conexão e localize o modelo ao examinar as colunas e os resultados previsíveis (por exemplo).  
  
     Usuários avançados: Se você estiver familiarizado com DMX ou XMLA, você pode copiar as instruções em um arquivo para uso posterior.  
  
3.  Quando você encontrar o nome do modelo temporário e da estrutura, abra **Gerenciar modelo** e selecione o modelo.  
  
4.  Clique em Exportar este modelo de mineração para gerar um arquivo de script em um local especificado por você.  
  
## <a name="see-also"></a>Consulte também  
 [Conectar-se à fonte de dados &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md)   
 [Utilitário de configuração do servidor &#40;Data Mining Add-ins para Excel&#41;](server-configuration-utility-data-mining-add-ins-for-excel.md)  
  
  
