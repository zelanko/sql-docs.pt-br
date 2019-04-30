---
title: 'Como fazer: Depurar Assemblies personalizados | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom assemblies [Reporting Services], debugging
- debugging custom assemblies [Reporting Services]
- troubleshooting [Reporting Services], custom assemblies
ms.assetid: 3a3215b3-548c-4474-81ba-3a98dd3912bf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 64a61e044c7ff6efe051eb316cb9f653f0993b68
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63265059"
---
# <a name="how-to-debug-custom-assemblies"></a>Como fazer: Depurar assemblies personalizados
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] fornece várias ferramentas de depuração que podem ajudar você a analisar o código de assembly personalizado e localizar erros nele. A melhor ferramenta a ser usada dependerá do que você estiver tentando realizar. Este exemplo usa o [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)].  
  
 A maneira recomendada de projetar, desenvolver e testar assemblies personalizados para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é criar uma solução que contenha os seus relatórios de teste e o seu assembly personalizado.  
  
### <a name="to-debug-assemblies-using-a-single-instance-of-visual-studio"></a>Para depurar assemblies usando uma única instância de Visual Studio  
  
1.  Crie um novo projeto de relatório usando o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
     No momento em que você cria um projeto de relatório, o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] também cria uma solução para contê-lo.  
  
2.  Adicione um novo projeto de Biblioteca de Classe à solução existente. Verifique se o projeto de relatório foi definido como o projeto de inicialização. Para obter mais informações sobre como realizar isso, consulte a documentação do seu [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
3.  No Gerenciador de Soluções, selecione a solução.  
  
4.  No menu **Exibir**, clique em **Página de Propriedades**.  
  
     A caixa de diálogo **Páginas de Propriedades da Solução** será aberta.  
  
5.  No painel esquerdo, expanda **Propriedades Comuns**, se necessário e clique em **Dependências do Projeto**. Selecione o projeto de relatório na lista suspensa **Projeto**. Selecione o projeto de assembly na lista **Depende De**.  
  
6.  Clique em **OK** para salvar as alterações e feche a caixa de diálogo **Páginas de Propriedades**.  
  
7.  No Gerenciador de Soluções, selecione o seu projeto de assembly personalizado.  
  
8.  No menu **Exibir**, clique em **Página de Propriedades**.  
  
     A caixa de diálogo **Páginas de Propriedades do Projeto** será exibida.  
  
9. Clique na guia **Criar** se você estiver em um projeto C# ou na guia **Compilar** se estiver em um projeto do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].  
  
10. Na página **Criar**/**Compilar**, insira o caminho para a pasta do Designer de Relatórios. Por padrão, o caminho é C:\Program Files\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE, que você deverá inserir na caixa de texto **Caminho de Saída**. Isso compilará e implantará uma versão atualizada do seu assembly personalizado diretamente no Designer de Relatórios antes da execução do seu relatório.  
  
11. Depois que você criar o seu relatório e desenvolver o seu assembly personalizado, defina os pontos de interrupção em seu código de assembly personalizado.  
  
12. Execute o relatório no modo **DebugLocal** pressionando a tecla F5. Quando o relatório for executado na janela pop-up de visualização, o depurador atingirá um dos pontos de interrupção que corresponda ao código executável em seu assembly. Use F11 para percorrer o seu código de assembly personalizado.  
  
### <a name="to-debug-assemblies-using-two-instances-of-visual-studio"></a>Para depurar assemblies usando duas instâncias do Visual Studio  
  
1.  Inicie o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e abra o seu projeto de assembly personalizado.  
  
2.  Crie o projeto e implante o seu assembly personalizado e o arquivo .pdb auxiliar no Designer de Relatórios. Para obter mais informações sobre a implantação, consulte [Implantando um assembly personalizado](deploying-a-custom-assembly.md).  
  
3.  Abra um projeto de relatório que use o seu assembly personalizado deixando o seu código de assembly personalizado aberto em uma instância separada do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
4.  Navegue até a instância do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] que contém o seu projeto de assembly personalizado e defina alguns pontos de quebra em seu código.  
  
5.  Com o projeto de assembly personalizado ainda na janela ativa, clique em **Anexar ao Processo** no menu **Depurar**.  
  
     A caixa de diálogo **Anexar ao Processo** será aberta.  
  
6.  Na lista de processos, selecione o processo devenv.exe que corresponde ao Projeto de Relatório e clique em **Anexar**.  
  
7.  Defina as expressões que serão usadas no relatório a partir do assembly personalizado e crie o relatório.  
  
8.  Quando terminar de criar o relatório, clique na guia **Visualizar**.  
  
     O relatório será executado e o código de assembly personalizado deve ser interrompido em seus pontos de quebra predefinidos.  
  
    > [!NOTE]  
    >  O uso da guia **Visualizar** não impõe permissões de código para o assembly. Para obter um teste completo, que inclui os erros de segurança de acesso do código, inicie o projeto de relatório na definição de configuração **DebugLocal**.  
  
9. Percorra seu código usando a tecla F11. Para obter mais informações sobre como depurar usando o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], consulte a documentação do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Usar assemblies personalizados com relatórios](using-custom-assemblies-with-reports.md)  
  
  
