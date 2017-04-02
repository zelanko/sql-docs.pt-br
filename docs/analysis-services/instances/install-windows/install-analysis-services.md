---
title: "Instalar o Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
caps.latest.revision: 20
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 19
---
# Instalar o Analysis Services
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] é um servidor de banco de dados analítico que hospeda modelos de tabela, cubos multidimensionais e modelos de mineração de dados que você pode acessar de relatórios, planilhas e painéis.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tem várias instâncias, o que significa que você pode instalar mais de uma cópia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] em um único computador ou executar versões novas e antigas lado a lado. Qualquer instância de instalação é executada em um dos três modos, conforme determinado durante a instalação: Multidimensional e Mineração de Dados, Tabular ou SharePoint. Se você quiser usar vários modos, você precisará de uma instância separada para cada um.  
  
 Depois de instalar o servidor em um modo específico, você poderá usá-lo para hospedar soluções que estejam em conformidade com esse modo. Por exemplo, um servidor de modo de tabela será exigido se você desejar acesso a dados de modelo de tabela pela rede.  
  
## Obter ferramentas e designers  
 A Instalação do SQL Server não instala mais as ferramentas de gerenciamento ou designers de modelo usados para design de soluções ou administração de servidor. Nesta versão, as ferramentas têm uma instalação separada, que você pode obter por meio dos links a seguir:  
  
-   [Baixar o SQL Server Management Studio para SQL Server 2016](https://msdn.microsoft.com/en-US/library/mt238290.aspx)  
  
-   [Download SQL Server Data Tools para SQL Server 2016](https://msdn.microsoft.com/en-US/library/mt204009.aspx)  
  
 Você precisará de ambos o Management Studio e o SQL Server Data Tools para trabalhar com dados e instâncias do Analysis Services. As ferramentas podem ser instaladas em qualquer lugar, mas não se esqueça de configurar as portas no servidor antes de tentar uma conexão. Veja [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) para obter detalhes.  
  
## Instalar usando um assistente  
 A lista a seguir mostra a você quais páginas no assistente de Instalação do SQL Server são usadas para instalar o Analysis Services.  
  
1.  Selecione o **Analysis Services** na Árvore de Recursos na Instalação.  
  
     ![Setup feature tree showing Analsyis Services](../../../analysis-services/instances/install-windows/media/ssas-setupas.gif "Setup feature tree showing Analsyis Services")  
  
2.  Na página Configuração do Analysis Services, selecione o **Modo de Tabela** se você desejar uma instância de tabela. Caso contrário, o padrão será o **modo Multidimensional e de Mineração de Dados**.  
  
     ![Setup page with Analysis Services config options](../../../analysis-services/instances/install-windows/media/ssas-setupasconfig.png "Setup page with Analysis Services config options")  
  
 O modo Multidimensional e Mineração de Dados usa MOLAP como o armazenamento padrão para modelos implantados no Analysis Services. Depois de implantar para o servidor, você pode configurar uma solução para usar o ROLAP para executar consultas diretamente no banco de dados relacional, em vez de armazenar dados de consulta em um banco de dados multidimensional do Analysis Services.  
  
 O modo Tabular usa o índice columnstore xVelocity de memória otimizada (VertiPaq), que é o armazenamento padrão para modelos tabulares que você implanta no Analysis Services. Depois de implantar soluções de modelo tabular no servidor, você pode configurar seletivamente soluções tabulares para usar o armazenamento em disco DirectQuery como uma alternativa ao armazenamento associada à memória.  
  
 O gerenciamento de memória e as configurações de E/S podem ser ajustados para obter um melhor desempenho ao usar modos de armazenamento não padrão. Veja [Propriedades do servidor do Analysis Services](../../../analysis-services/server-properties/server-properties-in-analysis-services.md) para obter mais informações.  
  
## Instalação de Linha de Comando  
 A Instalação do SQL Server inclui um parâmetro (**ASSERVERMODE**) que especifica o modo do servidor. O exemplo a seguir ilustra a instalação de linha de comando que instala o Analysis Services no modo de servidor Tabular.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 **INSTANCENAME** deve ter menos de 17 caracteres.  
  
 Todos os valores de conta de espaço reservado devem ser substituídos por contas e senhas válidas.  
  
 **ASSERVERMODE** diferencia maiúsculas de minúsculas.  Todos os valores devem ser expressos em maiúsculas. A tabela a seguir descreve os valores válidos para **ASSERVERMODE**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|MULTIDIMENSIONAL|Este é o valor padrão. Se você não configurar o **ASSERVERMODE**, o servidor será instalado no modo de servidor Multidimensional.|  
|POWERPIVOT|Esse valor é opcional. Na prática, se você configura o parâmetro **ROLE**, o modo de servidor é automaticamente definido como 1, tornando **ASSERVERMODE** opcional para um [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para uma instalação do SharePoint. Para obter mais informações, veja [Instalar Power Pivot por meio do Prompt de Comando](http://msdn.microsoft.com/pt-br/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328).|  
|TABULAR|Esse valor é obrigatório se você estiver instalando o Analysis Services no modo Tabular usando a instalação de linha de comando.|  
  
## Consulte também  
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Converter um banco de dados de tabela na memória para DirectQuery no SSMS &#40;SQL Server Management Studio&#41;](../Topic/Convert%20an%20in-memory%20Tabular%20Database%20to%20DirectQuery%20in%20SQL%20Server%20Management%20Studio%20\(SSMS\).md)   
 [Modelagem de tabela &#40;SSAS&#41;](../Topic/Tabular%20Modeling%20\(SSAS\).md)  
  
  