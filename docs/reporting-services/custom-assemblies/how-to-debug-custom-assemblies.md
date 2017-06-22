---
title: 'Como: depurar Assemblies personalizados | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom assemblies [Reporting Services], debugging
- debugging custom assemblies [Reporting Services]
- troubleshooting [Reporting Services], custom assemblies
ms.assetid: 3a3215b3-548c-4474-81ba-3a98dd3912bf
caps.latest.revision: 44
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b6cdc41f90765a3fc1a568bc76ddf0d41c15b38a
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="how-to-debug-custom-assemblies"></a>Como depurar assemblies personalizados
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] fornece várias ferramentas de depuração que podem ajudá-lo a analisar seu código de assembly personalizado e localizar erros nele. A melhor ferramenta a ser usada dependerá do que você estiver tentando realizar. Este exemplo usa o [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)].  
  
 A maneira recomendada de projetar, desenvolver e testar assemblies personalizados para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é criar uma solução que contenha os seus relatórios de teste e o seu assembly personalizado.  
  
### <a name="to-debug-assemblies-using-a-single-instance-of-visual-studio"></a>Para depurar assemblies usando uma única instância de Visual Studio  
  
1.  Crie um novo projeto de relatório usando o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
     No momento em que você cria um projeto de relatório, o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] também cria uma solução para contê-lo.  
  
2.  Adicione um novo projeto de Biblioteca de Classe à solução existente. Verifique se o projeto de relatório foi definido como o projeto de inicialização. Para obter mais informações sobre como realizar isso, consulte a documentação do seu [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
3.  No Gerenciador de Soluções, selecione a solução.  
  
4.  Sobre o **exibição** menu, clique em **páginas de propriedade**.  
  
     O **páginas de propriedade da solução** caixa de diálogo é aberta.  
  
5.  No painel esquerdo, expanda **propriedades comuns** se necessário e clique em **dependências do projeto**. Selecione o projeto de relatório o **projeto** lista suspensa. Selecione o seu projeto de assembly no **depende** lista.  
  
6.  Clique em **Okey** para salvar as alterações e fechar o **páginas de propriedade** caixa de diálogo.  
  
7.  No Gerenciador de Soluções, selecione o seu projeto de assembly personalizado.  
  
8.  Sobre o **exibição** menu, clique em **páginas de propriedade**.  
  
     O **páginas de propriedades do projeto** caixa de diálogo é aberta.  
  
9. Clique o **criar** guia se você estiver em um projeto c# ou o **compilar** guia se você estiver em um [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] projeto.  
  
10. No **criar**/**compilar** página, digite o caminho para a pasta do Designer de relatórios. Por padrão, isso é C:\Program Files\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE) no **caminho de saída** caixa de texto. Isso compilará e implantará uma versão atualizada do seu assembly personalizado diretamente no Designer de Relatórios antes da execução do seu relatório.  
  
11. Depois que você criar o seu relatório e desenvolver o seu assembly personalizado, defina os pontos de interrupção em seu código de assembly personalizado.  
  
12. Executar o relatório em **DebugLocal** modo pressionando a tecla F5. Quando o relatório for executado na janela pop-up de visualização, o depurador atingirá um dos pontos de interrupção que corresponda ao código executável em seu assembly. Use F11 para percorrer o seu código de assembly personalizado.  
  
### <a name="to-debug-assemblies-using-two-instances-of-visual-studio"></a>Para depurar assemblies usando duas instâncias do Visual Studio  
  
1.  Inicie o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e abra o seu projeto de assembly personalizado.  
  
2.  Crie o projeto e implante o seu assembly personalizado e o arquivo .pdb auxiliar no Designer de Relatórios. Para obter mais informações sobre a implantação, consulte [Implantando um Assembly personalizado](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md).  
  
3.  Abra um projeto de relatório que use o seu assembly personalizado deixando o seu código de assembly personalizado aberto em uma instância separada do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
4.  Navegue até a instância do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] que contém o seu projeto de assembly personalizado e defina alguns pontos de quebra em seu código.  
  
5.  Com o projeto de assembly personalizado ainda na janela ativa, clique em **anexar ao processo** no **depurar** menu.  
  
     O **anexar ao processo** caixa de diálogo é aberta.  
  
6.  Na lista de processos, selecione o processo devenv.exe que corresponde ao seu projeto de relatório e clique em **Attach**.  
  
7.  Defina as expressões que serão usadas no relatório a partir do assembly personalizado e crie o relatório.  
  
8.  Quando tiver terminado de criar seu relatório, clique no **visualização** guia.  
  
     O relatório será executado e o código de assembly personalizado deve ser interrompido em seus pontos de quebra predefinidos.  
  
    > [!NOTE]  
    >  Usando o **visualização** guia não impõe permissões de código para o assembly. Para um teste completo, que inclui quaisquer erros de segurança de acesso do código, inicie o projeto de relatório sob o **DebugLocal** configuração.  
  
9. Percorra seu código usando a tecla F11. Para obter mais informações sobre como depurar usando o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], consulte a documentação do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Usando assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
