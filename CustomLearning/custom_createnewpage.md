---
author: pkrebs
ms.author: pkrebs
title: Criar páginas do SharePoint para playlists
ms.date: 02/10/2019
description: Criar páginas do SharePoint para playlists
ms.service: sharepoint online
ms.openlocfilehash: 99425b9be685a8090394ecb446a7c82dee24fe5d
ms.sourcegitcommit: ee4aebf60893887ae95a1294a9ad8975539ea762
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "48234503"
---
# <a name="create-sharepoint-pages-for-custom-playlists"></a>Criar páginas do SharePoint para listas de reprodução personalizadas

Um dos recursos exclusivos dos caminhos de aprendizado é a capacidade de criar listas de reprodução remontadas de ativos da Microsoft e de ativos do SharePoint que você cria. Neste exemplo, criaremos uma página do SharePoint com antecedência da criação de uma lista de reprodução. A capacidade de criar listas de reprodução a partir de páginas do SharePoint oferece uma variedade de oportunidades para criar páginas usando as Web Parts disponíveis na Microsoft ou em sua organização. Por exemplo, uma lista de reprodução pode incluir uma página do SharePoint com vídeos incorporados do YouTube ou um formulário criado a partir de formulários do Office 365 ou um relatório incorporado do Power BI. Neste exemplo, mostraremos como criar uma página com a Web Part de inserção e a Web Part de texto.  

## <a name="create-a-sharepoint-page-for-a-custom-playlist"></a>Criar uma página do SharePoint para uma lista de reprodução personalizada

1. Clique no ícone de **engrenagem** do SharePoint e, em seguida, clique em **Adicionar uma página**.
2. Clique em **Adicionar uma nova seção (+)** no lado esquerdo da página e, em seguida, clique **duas colunas** para o layout da seção.
3. Na coluna à esquerda, clique em + e, em seguida, clique na Web Part de **incorporação** . 
4. Na coluna à direita, clique em + e, em seguida, clique na Web Part de **texto** . A página deve ter a seguinte aparência.

![cg-pagenewstart.png](media/cg-pagenewstart.png)

### <a name="add-a-video-and-text-from-youtube"></a>Adicionar um vídeo e um texto do YouTube

1. No navegador, vá para YouTube. Para este exemplo, pesquise por "What is Office 365 – Best Productivity aplicativos da Microsoft".
2. Clique no vídeo para reproduzi-lo, depois Pause-o e, em seguida, clique com o botão direito do mouse nele. 
3. Clique em **copiar código de inserção**e retorne para a página do SharePoint. 
4. Clique em **Adicionar código de incorporação** na Web Part de **incorporação** e, em seguida, adicione o código do vídeo do YouTube.
5. Retorne à página YouTube e copie o texto da **Descrição** do vídeo. 
6. Retorne à página do SharePoint, selecione a Web Part de **texto** e copie o texto do vídeo do YouTube.
7. Selecione o ícone **Editar Web Part** na área título da página do SharePoint e, em seguida, nomeie a página "introdução à playlist personalizada". 
8. Em **layout**, selecione **simples**e, em seguida, fechar painel de propriedades da **região de título** . A página agora deve ter a seguinte aparência. 

![cg-pagenewfinish.png](media/cg-pagenewfinish.png)

### <a name="publish-the-page"></a>Publicar a página

- Selecione o botão **publicar** . Agora você está pronto para adicionar esta página do SharePoint à sua lista de reprodução personalizada. 