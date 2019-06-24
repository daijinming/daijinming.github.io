- Using the Angular Router to navigate to external links
~~~

import { Directive, HostListener, ElementRef } from '@angular/core';
import { Router } from '@angular/router';
import { isNil } from 'ramda';

@Directive({
    selector: 'a[appExternalUrl]',
})
export class ExternalUrlDirective {
    constructor(private el: ElementRef, private router: Router) {}

    @HostListener('click', ['$event'])
    clicked(event: Event) {
        const url = this.el.nativeElement.href;
        if (isNil(url)) {
            return;
        }

        this.router.navigate(['/externalRedirect', { externalUrl: url }], {
            skipLocationChange: true,
        });

        event.preventDefault();
    }
}
~~~
