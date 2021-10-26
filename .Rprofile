local({
    ## function to find project root directory
    proj_root <- function ()
    {
        path <- normalizePath(".")
        suppressWarnings(
            system2("git", sprintf("-C %s rev-parse --show-toplevel",
                                   path), stdout = TRUE, stderr = TRUE)
        )
    }
    ls_dir <- getwd()
    setwd(proj_root())
    options(renv.config.sandbox.enabled = FALSE,
            renv.config.synchronized.check = FALSE)
    msg_fun <- if (interactive()) try else suppressMessages
    msg_fun({
        suppressWarnings(source("renv/activate.R"))
    })
    setwd(ls_dir)
})
