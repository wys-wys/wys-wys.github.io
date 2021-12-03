还是官方教程靠谱 

申请完成之后使用此命令安装证书

~/.acme.sh/acme.sh --installcert -d hk1.gcop.xyz --key-file /root/private.key --fullchain-file /root/cert.crt



# ZeroSSL.com CA

[Edit](https://github.com/acmesh-official/acme.sh/wiki/ZeroSSL.com-CA/_edit)[New Page](https://github.com/acmesh-official/acme.sh/wiki/_new)

ignoramous edited this page 10 days ago · [16 revisions](https://github.com/acmesh-official/acme.sh/wiki/ZeroSSL.com-CA/_history)

###  Pages 55

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">Home</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/Blogs-and-tutorials" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">Blogs and tutorials</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/BuyPass.com-CA" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">BuyPass.com CA</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/Change-default-CA-to-ZeroSSL" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">Change default CA to ZeroSSL</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/Creating-a-Debian-package" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">Creating a Debian package</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/Deploy-ssl-certs-to-apache-server" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">Deploy ssl certs to apache server</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/Deploy-ssl-certs-to-nginx" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">Deploy ssl certs to nginx</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/Deploy-ssl-to-SolusVM" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">Deploy ssl to SolusVM</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/deploy-to-docker-containers" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">deploy to docker containers</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/deployhooks" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">deployhooks</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/DNS-alias-mode" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">DNS alias mode</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/DNS-API-Dev-Guide" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">DNS API Dev Guide</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/DNS-API-Test" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">DNS API Test</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/DNS-manual-mode" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">DNS manual mode</a></div></summary></details>

- <details class="details-reset" style="box-sizing: border-box; display: block;"><summary style="box-sizing: border-box; display: list-item; cursor: pointer; list-style: none;"><div class="d-flex flex-items-start" style="box-sizing: border-box; align-items: flex-start !important; display: flex !important;"><div class="p-2 mt-n1 mb-n1 ml-n1 btn btn-octicon js-wiki-sidebar-toc-toggle-chevron-button " style="box-sizing: border-box; position: relative; display: inline-block; padding: 8px !important; font-size: 14px; font-weight: 500; line-height: 1; white-space: nowrap; vertical-align: middle; cursor: pointer; user-select: none; border: 0px; border-radius: 6px; appearance: none; color: var(--color-fg-muted); background: transparent; box-shadow: none; transition: color 0.2s cubic-bezier(0.3, 0, 0.5, 1) 0s, background-color, border-color; margin-left: -4px !important; margin-top: -4px !important; margin-bottom: -4px !important;"><span role="status" style="box-sizing: border-box;"><span class="sr-only" style="box-sizing: border-box; position: absolute; width: 1px; height: 1px; padding: 0px; overflow: hidden; clip: rect(0px, 0px, 0px, 0px); overflow-wrap: normal; border: 0px; margin: -1px; white-space: nowrap;">Loading</span></span><svg aria-hidden="true" height="16" viewBox="0 0 16 16" version="1.1" width="16" data-view-component="true" class="octicon octicon-triangle-down js-wiki-sidebar-toc-toggle-chevron  mr-0"><path d="M4.427 7.427l3.396 3.396a.25.25 0 00.354 0l3.396-3.396A.25.25 0 0011.396 7H4.604a.25.25 0 00-.177.427z"></path></svg></div><a class="flex-1 py-1 text-bold" href="https://github.com/acmesh-official/acme.sh/wiki/dnsapi" style="box-sizing: border-box; color: var(--color-accent-fg); text-decoration: none; background-color: transparent; flex-grow: 1 !important; flex-shrink: 1 !important; flex-basis: 0%; padding-top: 4px !important; padding-bottom: 4px !important; font-weight: 600 !important;">dnsapi</a></div></summary></details>

- Show 40 more pages…

[ Add a custom sidebar](https://github.com/acmesh-official/acme.sh/wiki/_new?wiki[name]=_Sidebar)

##### Clone this wiki locally



## Using ZeroSSL.com CA

ZeroSSL doesn't have rate limits. One can issue *unlimited* TLS/SSL certificate valid for 90 days ([ref](https://zerossl.com/letsencrypt-alternative/#acme)).

Note: Since `v3`, `acme.sh` uses Zerossl as the default Certificate Authority (CA). Account registration (one-time) is required before one can issue new certs. See also: https://github.com/acmesh-official/acme.sh/wiki/Change-default-CA-to-ZeroSSL

### 1. Register your account.

##### 1a. With an email address

```
acme.sh  --register-account  -m myemail@example.com --server zerossl
```

##### 1b. With EAB credentials

Alternatively, if you sign up for a [ZeroSSL account](https://app.zerossl.com/signup), bootstrap `acme.sh` with *External Account Binding* (EAB) credentials, like so:

1. Generate your EAB credentials from https://app.zerossl.com/developer
2. Register your EAB credentials.

```
acme.sh  --register-account  --server zerossl \
        --eab-kid  xxxxxxxxxxxx  \
        --eab-hmac-key  xxxxxxxxx
```

Users with a ZeroSSL account can manage issued certificates from [developer console](https://zerossl.com/features/console/).

### 2. Issue certificates

Use Zerossl.com with `--server zerossl`:

```
acme.sh --server zerossl  \
     --issue  -d  example.com \
     --dns dns_cf
```

If you don't want to specify `--server zerossl` every time you issue a cert, you can set `zerossl` as the default CA:

```
acme.sh --set-default-ca  --server zerossl
```

Read: https://github.com/acmesh-official/acme.sh/wiki/Server

Issue any cert *from* zerossl without having to specify `--server`:

```
acme.sh --issue -d  example.com --dns dns_cf
```

### 3. Troubleshooting

##### Le_OrderFinalize: A KeyID must be specified

If certificate issuance fails and you see something like this in the logs

```
[XYZ 18 09:50:07 -02 2020] Create new order error. Le_OrderFinalize not found. 
{"type":"urn:ietf:params:acme:error:malformed","status":400,"detail":"A Key ID MUST be specified"}
```

then, re-generate your EAB credentials (refer step #2) and [re-run certificate issuance](https://github.com/acmesh-official/acme.sh/wiki/How-to-issue-a-cert). See: [acme.sh/issues/3310](https://github.com/acmesh-official/acme.sh/issues/3310#issuecomment-785374480).

------



**Buy me a beer, Donate to \**acme.sh\** if it saves your time. Your donation makes \**acme.sh\** better: https://donate.acme.sh/**

如果 acme.sh 帮你节省了时间,请考虑赏我一杯啤酒🍺, 捐助: https://donate.acme.sh/ 你的支持将会使得 **acme.sh** 越来越好. 感谢

- © 2021 GitHub, Inc.
- [Terms](https://docs.github.com/en/github/site-policy/github-terms-of-service)
- [Privacy](https://docs.github.com/en/github/site-policy/github-privacy-statement)
- [Security](https://github.com/security)
- [Status](https://www.githubstatus.com/)
- [Docs](https://docs.github.com/)



- [Contact GitH](https://support.github.com/?tags=dotcom-footer)

# 使用acme申请https免费证书

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

文章标签： [运维](https://so.csdn.net/so/search/s.do?q=运维&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

### 前言

------

 上次写了一篇[https证书相关的笔记整理](https://juejin.im/post/5be2ab1a51882516d85b40c3),个人觉得有些地方欠妥,这次介绍一个更方便更简单更?一点的工具——acme.sh.上次使用的工具是certbot.

两者对比,acme.sh有如下优点:

- acme.sh会自动设置好定时任务.自动更新证书.certbot的更新需要手动设置cron.
- acme.sh可以使用域名解析商提供的 api 自动添加 txt 记录完成验证.简单、高效.
- 安装简单,没有环境依赖.卸载同样简单.

### 安装

------

```csharp
# 建议使用root安装,



curl  https://get.acme.sh | sh 



复制代码
```

该命令会把acme安装在~/.acme.sh路径下,并为你创建一个检查更新证书的定时任务.

因为该工具有个参数reloadcmd可以预设命令,可能会reload nginx服务器等.建议使用root安装.

```haskell
#查看定时任务



crontab -l



23 0 * * * "/root/.acme.sh"/acme.sh --cron --home "/root/.acme.sh" > /dev/null



# --home --cron参数解释可用~/.acme.sh/acme.sh -h查看,解释如下



  --home                   Specifies the home dir for acme.sh.指定acme的路径



  --cron                   Run cron job to renew all the certs.定时检查更新证书



复制代码
```

### 签发证书(Issue a cert)

------

签发证书前,需要验证域名的所有权,[acme支持多种方式验证](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2FNeilpang%2Facme.sh%2Fwiki%2FHow-to-issue-a-cert),建议使用http和dns验证.

我的个人域名解析使用的是cloudflare的free套餐,且acme文档写明支持cloudflare.所以选择dns验证.

依照[acme文档-how-to-use-dns-api](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2FNeilpang%2Facme.sh%2Fwiki%2Fdnsapi),

1.登录cloudflare官网获取API key.

```objectivec
#cloudflare-->个人配置--->API key - Global API Key - view API key



# 拿到API key后,设置如下环境变量.



export CF_Key="sdfsdfsdfljlbjkljlkjsdfoiwje"



export CF_Email="xxxx@sss.com"



复制代码
```

接下来就可以愉快的申请证书了.

**申请证书命令如下:**

```css
acme.sh --issue -d glc.im -d *.glc.im --dns dns_cf \ 



--key-file "/etc/nginx/ssl/glc.im/xxxx.key" \ 



--fullchain-file "/etc/nginx/ssl/fullchain.cer" \ 



--reloadcmd "service nginx reload"



复制代码
```

- glc.im /*.glc.im换成自己的域名
- dns_cf是对应的cloudflare,其他域名解析服务商请参照https://github.com/Neilpang/acme.sh/wiki/dnsapi
- key-file/fullchain-fil 签发证书后,acme会帮你把证书复制到该路径下
- reloadcmd 因为是root安装的acme 此命令可以帮助我重载nginx

### 更多内容

------

- **acme:** [github.com/Neilpang/ac…](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2FNeilpang%2Facme.sh%2Fwiki)
- 如何使githu page跳转到个人域名?
- 如何强制跳转https?

转载于:https://juejin.im/post/5c99142cf265da61103b5362

相关资源：[*acme*-companion:为Nginx代理自动生成*ACME*SSL*证书*-源码_*acme*.sh...](https://download.csdn.net/download/weixin_42175035/16630003?spm=1001.2101.3001.5697)



 

显示推荐内容



# 使用acme申请https免费证书

![img](https://csdnimg.cn/release/blogv2/dist/pc/img/reprint.png)

文章标签： [运维](https://so.csdn.net/so/search/s.do?q=运维&t=blog&o=vip&s=&l=&f=&viparticle=)

版权

### 前言

------

 上次写了一篇[https证书相关的笔记整理](https://juejin.im/post/5be2ab1a51882516d85b40c3),个人觉得有些地方欠妥,这次介绍一个更方便更简单更?一点的工具——acme.sh.上次使用的工具是certbot.

两者对比,acme.sh有如下优点:

- acme.sh会自动设置好定时任务.自动更新证书.certbot的更新需要手动设置cron.
- acme.sh可以使用域名解析商提供的 api 自动添加 txt 记录完成验证.简单、高效.
- 安装简单,没有环境依赖.卸载同样简单.

### 安装

------

```csharp
# 建议使用root安装,



curl  https://get.acme.sh | sh 



复制代码
```

该命令会把acme安装在~/.acme.sh路径下,并为你创建一个检查更新证书的定时任务.

因为该工具有个参数reloadcmd可以预设命令,可能会reload nginx服务器等.建议使用root安装.

```haskell
#查看定时任务



crontab -l



23 0 * * * "/root/.acme.sh"/acme.sh --cron --home "/root/.acme.sh" > /dev/null



# --home --cron参数解释可用~/.acme.sh/acme.sh -h查看,解释如下



  --home                   Specifies the home dir for acme.sh.指定acme的路径



  --cron                   Run cron job to renew all the certs.定时检查更新证书



复制代码
```

### 签发证书(Issue a cert)

------

签发证书前,需要验证域名的所有权,[acme支持多种方式验证](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2FNeilpang%2Facme.sh%2Fwiki%2FHow-to-issue-a-cert),建议使用http和dns验证.

我的个人域名解析使用的是cloudflare的free套餐,且acme文档写明支持cloudflare.所以选择dns验证.

依照[acme文档-how-to-use-dns-api](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2FNeilpang%2Facme.sh%2Fwiki%2Fdnsapi),

1.登录cloudflare官网获取API key.

```objectivec
#cloudflare-->个人配置--->API key - Global API Key - view API key



# 拿到API key后,设置如下环境变量.



export CF_Key="sdfsdfsdfljlbjkljlkjsdfoiwje"



export CF_Email="xxxx@sss.com"



复制代码
```

接下来就可以愉快的申请证书了.

**申请证书命令如下:**

```css
acme.sh --issue -d glc.im -d *.glc.im --dns dns_cf \ 



--key-file "/etc/nginx/ssl/glc.im/xxxx.key" \ 



--fullchain-file "/etc/nginx/ssl/fullchain.cer" \ 



--reloadcmd "service nginx reload"



复制代码
```

- glc.im /*.glc.im换成自己的域名
- dns_cf是对应的cloudflare,其他域名解析服务商请参照https://github.com/Neilpang/acme.sh/wiki/dnsapi
- key-file/fullchain-fil 签发证书后,acme会帮你把证书复制到该路径下
- reloadcmd 因为是root安装的acme 此命令可以帮助我重载nginx

### 更多内容

------

- **acme:** [github.com/Neilpang/ac…](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2FNeilpang%2Facme.sh%2Fwiki)
- 如何使githu page跳转到个人域名?
- 如何强制跳转https?

转载于:https://juejin.im/post/5c99142cf265da61103b5362

相关资源：[*acme*-companion:为Nginx代理自动生成*ACME*SSL*证书*-源码_*acme*.sh...](https://download.csdn.net/download/weixin_42175035/16630003?spm=1001.2101.3001.5697)



 

显示推荐内容