public ActionForward execute(ActionMapping mapping, ActionForm form, HttpServletRequest request,
        HttpServletResponse response) throws Exception {

    	// Create form
        ImportForm importForm = (ImportForm) form;
        
        WebApplicationContext context = WebApplicationContextUtils.getRequiredWebApplicationContext(this.getServlet().getServletContext());
		
        // Get CustomerService from context
		CustomerService customerService = (CustomerService) context.getBean("CustomerService");
		
        SearchForm searchForm = new SearchForm();
        
        searchForm.setCustomerName("");
        searchForm.setCustomerSex("");
        searchForm.setCustomerBirthdayFrom("");
        searchForm.setCustomerBirthdayTo("");
        
        // Search all Customer and store into list
        List<CustomerDto> list = customerService.search(searchForm);
        
        // Create session
        HttpSession session = request.getSession();
        
        // Clear all errors and messages
        errors.clear();
        messages.clear();
